# @recast-navigation/core

## 0.6.0

### Minor Changes

- 5e79ceb: feat(NavMesh): remove DebugNavMesh, change navMesh.getDebugNavMesh to return positions and indices arrays

### Patch Changes

- 5e79ceb: fix: debug nav mesh would not cover the whole nav mesh in some cases
- Updated dependencies [5e79ceb]
- Updated dependencies [5e79ceb]
  - @recast-navigation/wasm@0.6.0

## 0.5.0

### Minor Changes

- 820b928: BREAKING CHANGE: `generateSoloNavMesh` and `generateTiledNavMesh` no longer internally reverse input indices, this aligns the required input format with recast navigation c++ library itself (OpenGL conventions)

  The `generateSoloNavMesh` and `generateTiledNavMesh` were inadvertently reversing input indices. The three.js helpers `threeToSoloNavMesh` and `threeToTiledNavMesh` were also reversing indices so front faces would be walkable. This is likely an accidental leftover from using the BabylonJS recast plugin as the starting point of this library. Babylon at its core uses a left handed system.

  If you were previously using the `generateSoloNavMesh` and `generateTiledNavMesh` nav mesh generators, you will need to reverse your input indices to have a counter-clockwise winding order. If you were using the `recast-navigation/three` helpers, you do not need to change anything.

- 86554c1: feat(NavMesh): simplify `getPolyArea`, `getOffMeshConnectionsPolyEndPoints`, `addTile` return types
- 86554c1: feat(NavMeshQuery): change methods to have a `options` argument for optional filters, half extents, max sizes

### Patch Changes

- 5728e0c: feat: add 'type' to nav mesh generator intermediates object, either 'solo' or 'tiled'
- 86554c1: feat: move computePath logic out of cpp, into js using exposed dtNavMeshQuery functionality
- Updated dependencies [86554c1]
- Updated dependencies [86554c1]
  - @recast-navigation/wasm@0.5.0

## 0.4.1

### Patch Changes

- 0a1bf73: fix: raw types not resolving, not being included in docs

  Despite the fact that @recast-navigation/wasm is bundled into the core package, it still needs to be listed as a regular dependency so the types are available to the core package.

- Updated dependencies [0a1bf73]
  - @recast-navigation/wasm@0.4.1

## 0.4.0

### Minor Changes

- de28866: feat: change `NavMeshGenerator` to two exports, `generateSoloNavMesh` and `generateTiledNavMesh`
- de28866: feat: expose functionality for setting poly areas, poly flags, off mesh connections
- de28866: feat: expose more of dtNavMeshQuery via NavMeshQuery
- de28866: feat: overhaul `Raw` recast and detour bindings
- de28866: feat: remove `NavMeshExporter` and `NavMeshImporter` classes, export functions `exportNavMesh` and `importNavMesh`
- de28866: feat: implement builtin solo and tiled nav mesh generators in js with `Raw` api
- de28866: feat: expose dtCrowd directly, move majority of crowd logic from c++ to js
- de28866: feat: remove `emscripten` object, move functionality into `Raw` api

## 0.3.0

## 0.2.0

### Minor Changes

- cd82927: feat(NavMeshGenerator): split `generate` into `generateSoloNavMesh` and `generateTiledNavMesh`

## 0.1.2

### Patch Changes

- 273c456: feat: add destroy() methods to classes that need cleanup, address vec3 leaks

## 0.1.1

### Patch Changes

- b67eb8b: feat: make EXPECTED_LAYERS_PER_TILE and MAX_LAYERS constants configurable

## 0.1.0

### Minor Changes

- 44c71f0: feat: fix DebugNavMesh winding
- 44c71f0: feat: expose dtNavMesh methods and related classes

### Patch Changes

- 44c71f0: feat: add DtStatus constants and utils

## 0.0.7

### Patch Changes

- 87e768b: feat: split NavMesh into multiple classes, update helpers

  ### New Core Classes

  Functionality in the `NavMesh` class has been split into multiple classes that more closely mirror the recastnavigation api.

  - `TileCache`
    - Manages tiles and obstacles. Only used for tiled navmeshes.
  - `NavMeshQuery`
    - Provides methods for querying a navmesh.
  - `NavMeshExporter`
    - Methods for exporting a navmesh to a Uint8Array.
  - `NavMeshImporter`
    - Methods for importing a navmesh from a Uint8Array.
  - `NavMeshGenerator`
    - Methods for generating solo and tiled navmeshes.

  ### Changes to three.js utils and helpers

  The usage for `threeToNavMesh` has changed slightly to include the TileCache when generating a tiled navmesh.

  ```ts
  /* solo navmesh */
  const { navMesh } = threeToNavMesh(meshes);

  /* tiled navmesh */
  const { navMesh, tileCache } = threeToNavMesh(meshes, { tileSize: 16 });
  ```

  The `threeToNavMeshArgs` function has been renamed to `getPositionsAndIndices`.

  The helpers have also been updated to align with the new core classes:

  - `TileCacheHelper`
    - New helper for visualising obstacles in a `TileCache`
  - `NavMeshHelper`
    - `updateObstacles` has been moved to `TileCacheHelper`
  - `CrowdHelper`
    - `update` has been renamed to `updateAgents`, following the naming convention of the other helpers

- dfe1bcb: fix: walkable slope angle not affecting generated navmesh
- dfe1bcb: feat: add 'success' field to NavMeshGeneratorResult

## 0.0.6

### Patch Changes

- ad1adaa: feat: improve jsdoc

## 0.0.5

## 0.0.4

### Patch Changes

- 0e68563: feat: remove events, expose update methods on three helpers

## 0.0.3

### Patch Changes

- 05825a8: fix: make `@recast-navigation/wasm` a dev dependency of `@recast-navigation/core`.

  `@recast-navigation/wasm` is inlined in `@recast-navigation/core`'s build output, so it doesn't need to be a dependency of `@recast-navigation/core`.

## 0.0.2

### Patch Changes

- @recast-navigation/wasm@0.0.2

## 0.0.1

- Initial alpha release!
