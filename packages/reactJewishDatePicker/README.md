# react-jewish-datepicker

[![npm](https://badge.fury.io/js/react-jewish-datepicker.svg)](https://www.npmjs.com/package/react-jewish-datepicker)
[![CI](https://github.com/Shmulik-Kravitz/react-jewish-datepicker/workflows/CI/badge.svg?branch=master)](https://github.com/Shmulik-Kravitz/react-jewish-datepicker/)
![license](https://badgen.net/npm/license/react-jewish-datepicker)
![size](https://badgen.net/bundlephobia/min/react-jewish-datepicker)
![size minzip](https://badgen.net/bundlephobia/minzip/react-jewish-datepicker)
![downloads](https://badgen.net/npm/dt/react-jewish-datepicker)
[![stars](https://badgen.net/github/stars/Shmulik-Kravitz/react-jewish-datepicker)](https://github.com/Shmulik-Kravitz/react-jewish-datepicker/)
![open issues](https://badgen.net/github/open-issues/Shmulik-Kravitz/react-jewish-datepicker)
![watchers](https://badgen.net/github/watchers/Shmulik-Kravitz/react-jewish-datepicker)

![npm](https://raw.githubusercontent.com/Shmulik-Kravitz/react-jewish-datepicker/master/images/snapshot.png)

# ReactJewishDatePicker

General JewishDatePicker component.

See also [demo and documentation](https://react-jewish-datepicker.js.org/) page.

## Installation

```console
yarn add react-jewish-datepicker
```

Or with npm

```console
npm install react-jewish-datepicker --save
```

## Usage

#### TypeScript example:

```js
import * as React from "react";
import {
  ReactJewishDatePicker,
  BasicJewishDay,
  BasicJewishDate
} from "react-jewish-datepicker";

export default function App() {
  const [basicJewishDay, setBasicJewishDay] = React.useState<BasicJewishDay>();
  const basicJewishDate: BasicJewishDate = {
    day: 13,
    monthName: "Elul",
    year: 5788
  };

  return (
    <>
      <div>
        Hebrew:
        <ReactJewishDatePicker
          value={basicJewishDate}
          isHebrew
          onClick={(day: BasicJewishDay) => {
            setBasicJewishDay(day);
          }}
        />
      </div>
    </>
  );
}


```

[![Edit react-jewish-datepicker-typescript-example](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/react-jewish-datepicker-typescript-example-1myb0?fontsize=14&hidenavigation=1&theme=dark)

#### JavaScript example:

```js
import * as React from "react";
import { ReactJewishDatePicker, BasicJewishDay } from "react-jewish-datepicker";

export default function App() {
  const [basicJewishDay, setBasicJewishDay] = React.useState();
  return (
    <ReactJewishDatePicker
      value={new Date()}
      isHebrew
      onClick={(day) => {
        setBasicJewishDay(day);
      }}
    />
  );
}
```

[![Edit react-jewish-datepicker-javascript-example](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/pedantic-gagarin-rdeov?fontsize=14&hidenavigation=1&theme=dark)

## props

| Prop name | Description                                                                  | Value types                                                                                                                          |
| --------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| canSelect | Accepts a function which determines whether a day is selectable              | `(day: BasicJewishDay) => condition ? false : true`                                                                                  |
| isHebrew  | Optional. Whether the view language is hebrew or english, Default is `false` | `false` \| `true`                                                                                                                    |
| isRange   | Optional. Allow to select date ranges. Default is `false`                    | `false` \| `true`                                                                                                                    |
| onClick   | Callback when a date is selected                                             | `(day: BasicJewishDay) => console.log(day)` \| `(startDay: BasicJewishDay, endDay: BasicJewishDay) => console.log(startDay, endDay)` |
| value     | Optional. Initial selected date                                              | `Date` \| `BasicJewishDate` \| `BasicJewishDateRange` \| `DateRange`                                                                 |

### `canSelect` prop

The `canSelect` can take either a [`costum function`](https://react-jewish-datepicker.js.org/#disableWithCustomFunction) or one of the build-in functions as follows.

#### dontSelectHolidays([isIsrael: `boolean`]) ⇒ `(day: BasicJewishDay) => boolean`

Takes `isIsrael` param and returns a function which in turn is passed to the `canSelect` prop, in order to prevent holidays (corresponding with `isIsrael` param) selection.

| Param | Type   | Default |
| ----- | ------ | ----- |
| isIsrael  | `boolean` | `false` |

See example [here](https://react-jewish-datepicker.js.org/#disableHolidays)

#### dontSelectShabat(day: `BasicJewishDay`) ⇒ `boolean`

A function to be passed to the `canSelect` prop, in order to prevent shabat selection.

See example [here](https://react-jewish-datepicker.js.org/#disableShabat)

#### dontSelectShabatAndHolidays([isIsrael: `boolean`]) ⇒ `(day: BasicJewishDay) => boolean`

Takes `isIsrael` param and returns a function to be passed to the "canSelect" prop. combines `dontSelectHolidays` and `dontSelectShabat` in order to prevent both - shabat and holidays selection.

| Param | Type   | Default |
| ----- | ------ | ----- |
| isIsrael  | `boolean` | `false` |

See example [here](https://react-jewish-datepicker.js.org/#disableShabatAndHolidays)

#### dontSelectOutOfRange(minDate: `Date` | `null`, maxDate: `Date` | `null`) ⇒ `(day: BasicJewishDay) => boolean`

Takes min date and max date and returns a function to be passed to the "canSelect" prop, in order to prevent selection out of the supplied range.

You can pass a date only for one of the params and null to the other. In this case, the selectable range will be up to max date or from min date.

| Param | Type   |
| ----- | ------ |
| minDate  | `Date` \| `null` |
| maxDate  | `Date` \| `null` |

See example [here](https://react-jewish-datepicker.js.org/#selectionWithinRange)

### Helper Functions

#### addDates(date: `BasicJewishDate` | `Date`, numDays: `number`) ⇒ `Date`

a helper function for `dontSelectOutOfRange`.

Takes a `BasicJewishDate` object or a `Date`, adds a date interval (`numDays`) to the date and then returns the new date. 

| Param | Type   |
| ----- | ------ |
| date  | `BasicJewishDate` \| `Date` |
| numDays  | `number` |

See example [here](https://react-jewish-datepicker.js.org/#selectionWithinRange)

#### subtractDates(date: `BasicJewishDate` | `Date`, numDays: `number`) ⇒ `Date`

a helper function for `dontSelectOutOfRange`.

Takes a `BasicJewishDate` object or a `Date`, subtracts a date interval (`numDays`) from the date and then returns the new date.

| Param | Type   |
| ----- | ------ |
| date  | `BasicJewishDate` \| `Date` |
| numDays  | `number` |

See example [here](https://react-jewish-datepicker.js.org/#selectionWithinRange)

### jewish-dates-core

To create a jewish date picker in vue.js or angular, see the [core dependency](https://github.com/Shmulik-Kravitz/react-jewish-datepicker/blob/master/packages/jewishDatesCore/README.md).


## Contributors

- [Shmulik Kravitz](https://github.com/Shmulik-Kravitz)
- [Sagi Tawil](https://github.com/sagi770)
- [Yochanan Sheinberger](https://github.com/yochanan-sheinberger)
