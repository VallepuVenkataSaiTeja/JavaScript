# 2.5 Dates

## What is a Date?

A **Date** object in JavaScript represents a single moment in time. Internally, it stores the number of milliseconds elapsed since **January 1, 1970, 00:00:00 UTC** (the Unix epoch). Date objects are mutable and not thread-safe, but they're the standard way to work with dates in JavaScript.

```javascript
const now = new Date();
console.log(now);       // Current date/time
console.log(typeof now); // "object"
```

---

## 1. Creating Dates

### No Arguments: Current Date/Time
```javascript
const now = new Date();
console.log(now);
// Output: 2026-02-18T14:30:45.123Z (or local time)
```

### From Timestamp (Milliseconds Since Epoch)
```javascript
// Unix epoch
const epoch = new Date(0);
console.log(epoch);      // 1970-01-01T00:00:00.000Z

// Specific timestamp (ms)
const offset = new Date(1000);
console.log(offset);     // 1970-01-01T00:00:01.000Z

// Current timestamp
const now = new Date(Date.now());
console.log(now);

// Year 2000 (946684800000 ms after epoch)
const y2k = new Date(946684800000);
console.log(y2k);        // 2000-01-01T00:00:00.000Z
```

### From Year, Month, ... Arguments
```javascript
// new Date(year, month, day, hours, minutes, seconds, milliseconds)

// Year and month (month is 0-indexed!)
const date1 = new Date(2026, 1); // February 1, 2026
console.log(date1);

// Full date
const date2 = new Date(2026, 1, 18); // February 18, 2026
console.log(date2);

// With time
const date3 = new Date(2026, 1, 18, 14, 30, 45, 500);
console.log(date3);      // Feb 18, 2026, 14:30:45.500

// All parameters:
// year: 4-digit number (or 2-digit for 1900-1999)
// month: 0-11 (0 = Jan, 11 = Dec)
// day: 1-31 (default 1)
// hours: 0-23 (default 0)
// minutes: 0-59 (default 0)
// seconds: 0-59 (default 0)
// milliseconds: 0-999 (default 0)

// Example: New Year's Eve
const nye = new Date(2026, 11, 31, 23, 59, 59, 999);
console.log(nye);
```

### From Date String
```javascript
// ISO 8601 format (recommended)
const isoDate = new Date('2026-02-18');
console.log(isoDate);     // 2026-02-18T00:00:00.000Z

const isoFull = new Date('2026-02-18T14:30:45.123Z');
console.log(isoFull);     // 2026-02-18T14:30:45.123Z

// Various string formats (may vary by browser)
const formats = [
  new Date('2026-02-18'),
  new Date('02/18/2026'),
  new Date('February 18, 2026'),
  new Date('Feb 18, 2026'),
  new Date('Wed Feb 18 2026 14:30:45 GMT-0500')
];

// Invalid dates
const invalid = new Date('invalid string');
console.log(invalid);     // Invalid Date
console.log(isNaN(invalid)); // true
console.log(invalid.getTime()); // NaN
```

⚠️ **Warning**: String parsing is browser-dependent. Always use ISO 8601 format for consistency.

---

## 2. The Month Gotcha: 0-Indexed Months

### Months are 0-Based
This is famously unintuitive:

```javascript
// January = 0
const jan = new Date(2026, 0, 15);
console.log(jan); // January 15, 2026

// December = 11
const dec = new Date(2026, 11, 25);
console.log(dec); // December 25, 2026

// Common mistake
const feb = new Date(2026, 2, 15); // NOT February!
console.log(feb); // March 15, 2026 (month 2 = March)

// For February, use month 1
const realFeb = new Date(2026, 1, 18);
console.log(realFeb); // February 18, 2026
```

### Helper Function to Avoid This
```javascript
function dateWithNormalMonth(year, month, day, hours = 0, minutes = 0, seconds = 0) {
  return new Date(year, month - 1, day, hours, minutes, seconds);
}

const feb = dateWithNormalMonth(2026, 2, 15); // 1-based month
console.log(feb); // February 15, 2026 (correct!)

const dec = dateWithNormalMonth(2026, 12, 25); // December
console.log(dec); // December 25, 2026
```

---

## 3. Getting Date Components

### Local Time Getters

```javascript
const date = new Date('2026-02-18T14:30:45.123');

// Year
console.log(date.getFullYear());       // 2026
console.log(date.getYear());           // 126 (deprecated, avoid)

// Month (0-indexed!)
console.log(date.getMonth());          // 1 (February)

// Day of month
console.log(date.getDate());           // 18

// Day of week (0-indexed, 0 = Sunday)
console.log(date.getDay());            // 3 (Wednesday)

// Time components
console.log(date.getHours());          // 14
console.log(date.getMinutes());        // 30
console.log(date.getSeconds());        // 45
console.log(date.getMilliseconds());   // 123

// Milliseconds since epoch
console.log(date.getTime());           // 1766091045123
```

### Helper to Get Day Name
```javascript
const dayNames = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
const date = new Date('2026-02-18');
const dayIndex = date.getDay();
console.log(dayNames[dayIndex]); // 'Wednesday'

// Or for months
const monthNames = ['January', 'February', 'March', 'April', 'May', 'June',
                    'July', 'August', 'September', 'October', 'November', 'December'];
const monthIndex = date.getMonth();
console.log(monthNames[monthIndex]); // 'February'
```

### UTC Variants

Get components in UTC time (not affected by time zone):

```javascript
const date = new Date('2026-02-18T14:30:45.123Z');

// UTC getters
console.log(date.getUTCFullYear());    // 2026
console.log(date.getUTCMonth());       // 1 (still 0-indexed)
console.log(date.getUTCDate());        // 18
console.log(date.getUTCDay());         // 3
console.log(date.getUTCHours());       // 14
console.log(date.getUTCMinutes());     // 30
console.log(date.getUTCSeconds());     // 45
console.log(date.getUTCMilliseconds()); // 123

// Difference
const localDate = new Date('2026-02-18T14:30:45');
console.log(localDate.getHours());     // 14 (local time)
console.log(localDate.getUTCHours());  // May differ (depends on time zone)
```

---

## 4. Setting Date Components

### Local Time Setters

```javascript
const date = new Date();

// Modify year
date.setFullYear(2027);

// Modify month (0-indexed)
date.setMonth(11); // December

// Modify day
date.setDate(25);

// Modify time
date.setHours(23);
date.setMinutes(59);
date.setSeconds(59);
date.setMilliseconds(999);

console.log(date); // Shows the modified date
```

### UTC Variants

```javascript
const date = new Date();

date.setUTCFullYear(2027);
date.setUTCMonth(11);
date.setUTCDate(25);
date.setUTCHours(23);
date.setUTCMinutes(59);
date.setUTCSeconds(59);
date.setUTCMilliseconds(999);

console.log(date);
```

### Return Value
Setters return the timestamp:

```javascript
const date = new Date();
const timestamp = date.setFullYear(2027);
console.log(timestamp); // Milliseconds since epoch
```

---

## 5. Timestamps

### What is a Timestamp?

A **timestamp** is the number of **milliseconds** since January 1, 1970, 00:00:00 UTC (Unix epoch).

```javascript
const date = new Date('2026-02-18T14:30:45.123Z');

// Get timestamp
const timestamp = date.getTime();
console.log(timestamp);    // 1766091045123

// Create from timestamp
const fromTimestamp = new Date(1766091045123);
console.log(fromTimestamp); // 2026-02-18T14:30:45.123Z
```

### `Date.now()`
Returns current timestamp (cannot instantiate Date.now without `new`):

```javascript
// Get current timestamp
const now = Date.now();
console.log(now);          // e.g., 1766091045123

// Equivalent to
const now2 = new Date().getTime();
console.log(now2);         // Same value

// Performance measurement
const start = Date.now();
// ... do something slow ...
const end = Date.now();
const duration = end - start;
console.log(`Operation took ${duration}ms`);
```

### Timestamp Calculations

Timestamps are useful for arithmetic since they're just numbers:

```javascript
const now = new Date();
const nowTime = now.getTime();

// Add 1 hour (3600000 ms)
const inOneHour = new Date(nowTime + 3600000);
console.log(inOneHour);

// Subtract 1 day (86400000 ms)
const yesterday = new Date(nowTime - 86400000);
console.log(yesterday);

// Add 1 week (604800000 ms)
const nextWeek = new Date(nowTime + 604800000);
console.log(nextWeek);

// Simpler with constants
const MS_PER_SECOND = 1000;
const MS_PER_MINUTE = 60 * 1000;
const MS_PER_HOUR = 60 * 60 * 1000;
const MS_PER_DAY = 24 * 60 * 60 * 1000;

const inTwo = new Date(nowTime + 2 * MS_PER_HOUR);
console.log(inTwo); // 2 hours from now
```

### Compare Dates Using Timestamps

```javascript
const date1 = new Date('2026-02-18');
const date2 = new Date('2026-03-01');

const time1 = date1.getTime();
const time2 = date2.getTime();

if (time1 < time2) {
  console.log('date1 is before date2');
}

const diff = time2 - time1; // milliseconds
const days = diff / (1000 * 60 * 60 * 24);
console.log(`${days} days apart`);
```

---

## 6. Formatting Dates

### `toISOString()`
Returns ISO 8601 string (always UTC, ends with Z):

```javascript
const date = new Date('2026-02-18T14:30:45.123');

const isoString = date.toISOString();
console.log(isoString);    // '2026-02-18T14:30:45.123Z'

// Always formatted as YYYY-MM-DDTHH:mm:ss.sssZ
// Useful for APIs and storage

// Parse back
const parsed = new Date(isoString);
console.log(parsed);
```

### `toString()` and `toUTCString()`
```javascript
const date = new Date('2026-02-18T14:30:45.123');

// Local string (browser-dependent format)
console.log(date.toString());
// e.g., "Wed Feb 18 2026 14:30:45 GMT-0500 (Eastern Standard Time)"

// UTC string
console.log(date.toUTCString());
// e.g., "Wed, 18 Feb 2026 19:30:45 GMT"
```

### `toLocaleString()`, `toLocaleDateString()`, `toLocaleTimeString()`

Format dates according to locale:

```javascript
const date = new Date('2026-02-18T14:30:45');

// Locale-aware full format
console.log(date.toLocaleString());     // e.g., "2/18/2026, 2:30:45 PM"
console.log(date.toLocaleString('en-GB')); // e.g., "18/02/2026, 14:30:45"
console.log(date.toLocaleString('de-DE')); // e.g., "18.2.2026, 14:30:45"

// Date only
console.log(date.toLocaleDateString()); // e.g., "2/18/2026"
console.log(date.toLocaleDateString('en-GB')); // e.g., "18/02/2026"
console.log(date.toLocaleDateString('fr-FR')); // e.g., "18/02/2026"

// Time only
console.log(date.toLocaleTimeString()); // e.g., "2:30:45 PM"
console.log(date.toLocaleTimeString('en-GB')); // e.g., "14:30:45"
```

### Options for Localization

```javascript
const date = new Date('2026-02-18T14:30:45');

// Custom format options
const options = {
  weekday: 'long',       // 'Monday', 'Tuesday', etc.
  year: 'numeric',       // '2026'
  month: 'long',         // 'February'
  day: 'numeric',        // '18'
  hour: '2-digit',       // '14'
  minute: '2-digit',     // '30'
  second: '2-digit',     // '45'
  timeZone: 'UTC'        // Use specific timezone
};

console.log(date.toLocaleString('en-US', options));
// "Wednesday, February 18, 2026, 14:30:45"

const dateOnly = {
  weekday: 'short',      // 'Mon'
  month: 'short',        // 'Feb'
  day: '2-digit'         // '18'
};
console.log(date.toLocaleDateString('en-US', dateOnly));
// "Wed, Feb 18"
```

### Custom Formatting Helper

```javascript
function formatDate(date, format = 'YYYY-MM-DD') {
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, '0');
  const day = String(date.getDate()).padStart(2, '0');
  const hours = String(date.getHours()).padStart(2, '0');
  const minutes = String(date.getMinutes()).padStart(2, '0');
  const seconds = String(date.getSeconds()).padStart(2, '0');

  const replacements = {
    'YYYY': year,
    'MM': month,
    'DD': day,
    'HH': hours,
    'mm': minutes,
    'ss': seconds
  };

  let result = format;
  for (const [key, value] of Object.entries(replacements)) {
    result = result.replace(key, value);
  }
  return result;
}

const date = new Date('2026-02-18T14:30:45');
console.log(formatDate(date, 'YYYY-MM-DD'));        // '2026-02-18'
console.log(formatDate(date, 'DD/MM/YYYY'));        // '18/02/2026'
console.log(formatDate(date, 'YYYY-MM-DD HH:mm:ss')); // '2026-02-18 14:30:45'
```

---

## 7. Date Manipulation

### Important: Dates are Mutable

```javascript
const original = new Date('2026-02-18');
const modified = original;

modified.setDate(25);

console.log(original); // Also February 25 (same object)
console.log(modified); // February 25
```

### Copy a Date Before Modifying

```javascript
const original = new Date('2026-02-18');

// Create a copy
const copy = new Date(original.getTime());
copy.setDate(25);

console.log(original); // Still February 18
console.log(copy);     // February 25
```

### Add Time Using Timestamp Math

Since JavaScript Date has no built-in add/subtract, use timestamps:

```javascript
const date = new Date('2026-02-18T14:30:00');

// Helper function
function addTime(date, milliseconds) {
  return new Date(date.getTime() + milliseconds);
}

// Add 1 second
const inOneSecond = addTime(date, 1000);
console.log(inOneSecond);

// Add 5 minutes
const inFiveMinutes = addTime(date, 5 * 60 * 1000);
console.log(inFiveMinutes);

// Add 1 day
const tomorrow = addTime(date, 24 * 60 * 60 * 1000);
console.log(tomorrow);
```

### Subtract Time

```javascript
function subtractTime(date, milliseconds) {
  return new Date(date.getTime() - milliseconds);
}

const date = new Date('2026-02-18T14:30:00');

const yesterday = subtractTime(date, 24 * 60 * 60 * 1000);
console.log(yesterday); // February 17

const anHourAgo = subtractTime(date, 60 * 60 * 1000);
console.log(anHourAgo);
```

### Add/Subtract Months (Tricky)

```javascript
function addMonths(date, months) {
  const newDate = new Date(date);
  newDate.setMonth(newDate.getMonth() + months);
  return newDate;
}

const date = new Date('2026-02-18');

const nextMonth = addMonths(date, 1);
console.log(nextMonth); // March 18

const next3Months = addMonths(date, 3);
console.log(next3Months); // May 18

// Gotcha: adding 1 month to Jan 31 gives Feb 28/29!
const jan31 = new Date('2026-01-31');
const feb31 = addMonths(jan31, 1);
console.log(feb31); // March 3 (not Feb 31)
```

### Calculate Age in Years

```javascript
function getAge(birthDate) {
  const today = new Date();
  let age = today.getFullYear() - birthDate.getFullYear();
  
  // Adjust if birthday hasn't occurred this year
  const monthDiff = today.getMonth() - birthDate.getMonth();
  if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birthDate.getDate())) {
    age--;
  }
  
  return age;
}

const birthDate = new Date('1990-05-15');
console.log(getAge(birthDate)); // Current age
```

---

## 8. Time Zones

### Local vs UTC

JavaScript Date internally stores UTC time but displays in local time:

```javascript
const date = new Date('2026-02-18T14:30:00Z'); // UTC

// Local time (depends on system time zone)
console.log(date.getHours());       // e.g., 9 (EST)
console.log(date.getMinutes());     // 30

// UTC time
console.log(date.getUTCHours());    // 14
console.log(date.getUTCMinutes());  // 30
```

### Time Zone Offset

```javascript
const date = new Date();

// Get offset in minutes (negative for west of UTC)
const offsetMinutes = date.getTimezoneOffset();
console.log(offsetMinutes); // e.g., -300 (EST is UTC-5, so -5*60)

// Convert to hours
const offsetHours = offsetMinutes / 60;
console.log(offsetHours); // e.g., -5
```

### String Format with Time Zone

```javascript
const date = new Date('2026-02-18T14:30:45');

// toISOString() always uses UTC
console.log(date.toISOString());  // '2026-02-18T...:Z'

// toUTCString() shows UTC
console.log(date.toUTCString());  // 'Wed, 18 Feb 2026 14:30:45 GMT'

// toString() shows local time zone
console.log(date.toString());     // Includes time zone like 'GMT-0500'
```

### Create Date from Specific Timezone

⚠️ **Important**: JavaScript Date doesn't have built-in timezone support beyond UTC.

For specific timezone handling, you need external libraries like **date-fns** or **Day.js**:

```javascript
// This is NOT supported natively:
// new Date('2026-02-18T14:30:00', 'America/New_York')

// But you can use toLocaleString with timeZone option
const date = new Date('2026-02-18T14:30:00Z');
const nycTime = date.toLocaleString('en-US', {
  timeZone: 'America/New_York'
});
console.log(nycTime); // Time in NYC

// However, this rounds to seconds and returns a string, not a Date
```

### Limitations of Built-in Date

1. **No timezone support in constructor** — Can't create date in specific timezone
2. **Only UTC aware** — No daylight saving time handling
3. **String parsing is unreliable** — Different behavior across browsers
4. **No built-in formatting** — Must use `toLocaleString()` or custom functions
5. **Month is 0-indexed** — Confusing API
6. **Milliseconds precision** — Some systems need microseconds

For serious date/time work, use:
- **date-fns** — Lightweight, functional
- **Day.js** — Minimalist, chainable
- **Moment.js** — Heavy-featured (not recommended for new projects)

---

## 9. Practical Examples

### Check if Valid Date

```javascript
function isValidDate(date) {
  return date instanceof Date && !isNaN(date.getTime());
}

console.log(isValidDate(new Date()));           // true
console.log(isValidDate(new Date('2026-02-18'))); // true
console.log(isValidDate(new Date('invalid')));  // false
console.log(isValidDate('2026-02-18'));        // false (string, not Date)
```

### Compare Dates

```javascript
function isBefore(date1, date2) {
  return date1.getTime() < date2.getTime();
}

function isAfter(date1, date2) {
  return date1.getTime() > date2.getTime();
}

function isSameDay(date1, date2) {
  return date1.getFullYear() === date2.getFullYear() &&
         date1.getMonth() === date2.getMonth() &&
         date1.getDate() === date2.getDate();
}

const d1 = new Date('2026-02-18');
const d2 = new Date('2026-02-19');

console.log(isBefore(d1, d2));  // true
console.log(isSameDay(d1, d1)); // true
```

### Check if Date is Today

```javascript
function isToday(date) {
  const today = new Date();
  return date.getFullYear() === today.getFullYear() &&
         date.getMonth() === today.getMonth() &&
         date.getDate() === today.getDate();
}

console.log(isToday(new Date()));
console.log(isToday(new Date('2026-02-18')));
```

### Days Between Dates

```javascript
function daysBetween(date1, date2) {
  const MS_PER_DAY = 1000 * 60 * 60 * 24;
  const diff = Math.abs(date2.getTime() - date1.getTime());
  return Math.floor(diff / MS_PER_DAY);
}

const d1 = new Date('2026-02-18');
const d2 = new Date('2026-02-25');

console.log(daysBetween(d1, d2)); // 7
```

### Check if Leap Year

```javascript
function isLeapYear(year) {
  return (year % 4 === 0 && year % 100 !== 0) || (year % 400 === 0);
}

// Or use Date
function isLeapYearDate(date) {
  const year = date.getFullYear();
  return isLeapYear(year);
}

const date = new Date('2024-02-29');
console.log(isLeapYearDate(date)); // true (2024 is leap year)

const date2 = new Date('2026-02-18');
console.log(isLeapYearDate(date2)); // false (2026 is not)
```

### Count Down Timer

```javascript
function getCountdown(targetDate) {
  const now = new Date();
  const diff = targetDate.getTime() - now.getTime();

  if (diff <= 0) return 'Event has started!';

  const days = Math.floor(diff / (1000 * 60 * 60 * 24));
  const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
  const seconds = Math.floor((diff % (1000 * 60)) / 1000);

  return `${days}d ${hours}h ${minutes}m ${seconds}s`;
}

const newYear = new Date('2027-01-01');
console.log(getCountdown(newYear)); // e.g., "347d 9h 29m 15s"
```

---

## Summary: Date Methods Quick Reference

| Getter | UTC Variant | Purpose |
|--------|-------------|---------|
| `getFullYear()` | `getUTCFullYear()` | Get year |
| `getMonth()` | `getUTCMonth()` | Get month (0-11) |
| `getDate()` | `getUTCDate()` | Get day (1-31) |
| `getDay()` | `getUTCDay()` | Get weekday (0-6) |
| `getHours()` | `getUTCHours()` | Get hours (0-23) |
| `getMinutes()` | `getUTCMinutes()` | Get minutes (0-59) |
| `getSeconds()` | `getUTCSeconds()` | Get seconds (0-59) |
| `getMilliseconds()` | `getUTCMilliseconds()` | Get milliseconds (0-999) |
| `getTime()` | — | Get timestamp (ms) |

| Setter | UTC Variant | Purpose |
|--------|-------------|---------|
| `setFullYear()` | `setUTCFullYear()` | Set year |
| `setMonth()` | `setUTCMonth()` | Set month (0-11) |
| `setDate()` | `setUTCDate()` | Set day (1-31) |
| `setHours()` | `setUTCHours()` | Set hours (0-23) |
| `setMinutes()` | `setUTCMinutes()` | Set minutes (0-59) |
| `setSeconds()` | `setUTCSeconds()` | Set seconds (0-59) |
| `setMilliseconds()` | `setUTCMilliseconds()` | Set milliseconds (0-999) |
| `setTime()` | — | Set timestamp (ms) |

---

## Best Practices

✅ **Always use ISO 8601 format for date strings** — `'2026-02-18T14:30:45Z'`

✅ **Use `getTime()` or `Date.now()` for comparisons** — More reliable than comparing Date objects

✅ **Store dates as UTC in databases** — Convert to local on display

✅ **Remember months are 0-indexed** — Add a comment or use helper function

✅ **Use `toISOString()` for APIs** — Standard format across platforms

✅ **Copy dates before modifying** — Dates are mutable

✅ **Use timestamp math for arithmetic** — No built-in add/subtract

✅ **Consider external libraries for timezone work** — date-fns, Day.js

---

## Common Gotchas

❌ **Months are 0-indexed**
```javascript
new Date(2026, 1, 18); // February (not January!)
// Should be new Date(2026, 1, 18) for Feb
```

❌ **Date objects are mutable**
```javascript
const d1 = new Date('2026-02-18');
const d2 = d1;
d2.setDate(25);
console.log(d1); // Also February 25 (same object!)
// Always copy: const d2 = new Date(d1.getTime());
```

❌ **String parsing is unreliable**
```javascript
// Different results in different browsers/locales
new Date('02/18/2026');  // May be Feb 18 or invalid
// Always use ISO: new Date('2026-02-18')
```

❌ **No timezone support in constructor**
```javascript
// Can't create date for specific timezone
new Date('2026-02-18', 'America/New_York'); // Doesn't work
// Use extern library or toLocaleString() with timeZone option
```

❌ **Timestamps are in milliseconds, not seconds**
```javascript
const timestamp = 1766091045; // This is wrong (seconds)
const correct = 1766091045000; // Milliseconds
```

❌ **Comparing Date objects directly**
```javascript
new Date('2026-02-18') === new Date('2026-02-18'); // false!
// Compare timestamps: date1.getTime() === date2.getTime()
```

❌ **Forget to use `new` with Date()**
```javascript
const date = Date(); // Returns string, not Date object
// Correct: const date = new Date();
```
