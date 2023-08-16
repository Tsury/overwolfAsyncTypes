# overwolf-async-types

Async, typed wrapper for the [Overwolf API](https://github.com/overwolf/types).

## Install

To install, run:

\`\`\`bash
npm install overwolf-async-types
\`\`\`

## Usage

1. Add the types to your `tsconfig.json` file:

\`\`\`javascript
{
  "compilerOptions": {
    "types": [
      "overwolf-async-types/index.d.ts"
    ]
  }
}
\`\`\`

2. Call the `promisify` method before using the Overwolf API:

\`\`\`javascript
import { promisify } from 'overwolf-async-types';

promisify();
\`\`\`

3. Consume the API using Promises:

\`\`\`javascript
const res = await overwolf.windows.obtainDeclaredWindow('main');
\`\`\`

## How Does It Work

1. Fetches the latest d.ts files from Overwolf's repo
2. Iterates the types inside `overwolf.d.ts` and updates it to use Promises, also updates JSDoc accordingly.
3. Generates promisify code into `promisify.js` - this code traverses the Overwolf API during runtime and wraps relevant functions in a Promise.

## Notes

- To prevent conflicts, make sure you remove Overwolf's types library (`@overwolf/types`).
- Some Overwolf functions are readonly (e.g. `overwolf.io.dir`) - Those functions are kept intact, and new functions with an `Async` suffix are added (e.g. `overwolf.io.dirAsync`)
- This solution only converts functions with a last parameter with a name `callback` and type `CallbackFunction`. There are some rare cases of callbacks either appearing not as the last param, or not having the exact name `callback`. Those functions are left untouched. If you want to add functionaliy to support these rare cases, please make a PR.
- Currently it seems that the official definitions file is not fully up-to-date with the actual API. If you find any discrepancies, open a PR on Overwolf's repo. I have contacted Overwolf and they are working on a way to generate the types out of their codebase to ensure coherence.
- This repo was created to serve my needs - it's not guaranteed to work for you OOTB. If you encounter any issues, don't hesitate to either open an issue or create a PR. 