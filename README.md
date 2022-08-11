# Vitest Mocks for Google Maps

[![npm](https://img.shields.io/npm/v/@demissew/google-maps-vitest-mocks)](https://www.npmjs.com/package/@demissew/google-maps-vitest-mocks)
![Build](https://github.com/demissew/google-maps-vitest-mocks/workflows/Test/badge.svg)
![Release](https://github.com/demissew/google-maps-vitest-mocks/workflows/Release/badge.svg)
![GitHub contributors](https://img.shields.io/github/contributors/demissew/google-maps-vitest-mocks?color=green)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)


## Description

Vitest mocks for Google Maps in TypeScript.

**Note:** If you find a missing mock, please open an [issue][issues].

## NPM

Available via NPM as the package `@demissew/google-maps-vitest-mocks`

## Inspecting mocks

You can inspect what happens with the created mock instances (e.g. `Map` or `Marker`) via the `mockInstances` object.

```ts
import { initialize, Map, Marker, mockInstances } from "@demissew/google-maps-vitest-mocks";

beforeEach(() => {
  initialize();
});

test("my test", () => {
  const map = new google.maps.Map(null);
  const markerOne = new google.maps.Marker();
  const markerTwo = new google.maps.Marker();

  map.setHeading(8);
  markerOne.setMap(map);
  markerTwo.setLabel("My marker");

  const mapMocks = mockInstances.get(Map);
  const markerMocks = mockInstances.get(Marker);

  expect(mapMocks).toHaveLength(1);
  expect(markerMocks).toHaveLength(2);
  expect(mapMocks[0].setHeading).toHaveBeenCalledWith(8);
  expect(markerMocks[0].setMap).toHaveBeenCalledTimes(1);
  expect(markerMocks[1].setLabel).toHaveBeenCalledWith("My marker");
});
```

## Cleaning up mocks

Whenever `initialize()` is called, the captured mocks are automatically cleaned. Using any of Vitest's methods, you can clean the mock instances at any time:

```ts
import { initialize, Map, Marker, mockInstances } from "@demissew/google-maps-vitest-mocks";

beforeAll(() => {
  initialize();
});

// Clear all mocks
beforeEach(() => {
  mockInstances.clearAll();
});

// Clear specific mocks
beforeEach(() => {
  mockInstances.clear(Map, Marker);
});
```

## Support

This library is community supported. We're comfortable enough with the stability and features of
the library that we want you to build real production applications on it.

If you find a bug, or have a feature suggestion, please [log an issue][issues]. If you'd like to
contribute, please read [How to Contribute][contrib].

[issues]: https://github.com/demissew/google-maps-vitest-mocks/issues
[contrib]: CONTRIBUTING.md
