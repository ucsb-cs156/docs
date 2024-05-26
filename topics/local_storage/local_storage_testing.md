---
parent: GitHub
grand_parent: Topics
layout: default
title: "Local Storage: Testing"
description:  "how to write jest tests involving local storage"
---

# {{page.title}} - {{page.description}}

Here are some examples of writing jest tests that involve local storage.

## Disclaimer about code examples

Keep in mind that all code examples on this page were up-to-date at the time they were posted, but that the
code base is ever changing.  We have used "github permalinks" to link to the source code *as it was* at the time
these were collated.

## Clearing `localStorage` in `beforeEach`

You may want to clear `localStorage` in the `beforeEach` of your test so that each test starts from empty local storage.

This example is from [frontend/src/tests/components/PersonalSchedules/PersonalScheduleSelector.test.js](https://github.com/ucsb-cs156/proj-courses/blob/55f42a4f2d31dd0b785e51bf23a202ce82add854/frontend/src/tests/components/PersonalSchedules/PersonalScheduleSelector.test.js#L12)

```js
 beforeEach(() => {
    localStorage.clear();
    // ... other code might go here
  });
```

## Mocking `localStorage` 

You can use this lines of code to create a jest `mock` for localStorage:

```js
    const getItemSpy = jest.spyOn(Storage.prototype, "getItem");
```

If you want your mock to always return a specific value, say `"1"`, you can create a mock implementation:

```
    getItemSpy.mockImplementation(() => "1");
```

If your mock implementation needed to be more sophisticated, you could set up an object with the mapping of what you expect to be in `localStorage`,
and then return `null` if the key is not found:

```
    getItemSpy.mockImplementation((key) => {
       const values = {
         "key1" : "value1",
         "key2" : "value2"
       }
       return ( key in values ? values[key] : null );
    });
```

