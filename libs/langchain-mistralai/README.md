# @langchain/mistralai

This package contains the LangChain.js integrations for Mistral through their SDK.

## Installation

```bash npm2yarn
npm install @langchain/mistralai
```

This package, along with the main LangChain package, depends on [`@langchain/core`](https://npmjs.com/package/@langchain/core/).
If you are using this package with other LangChain packages, you should make sure that all of the packages depend on the same instance of @langchain/core.
You can do so by adding appropriate field to your project's `package.json` like this:

```json
{
  "name": "your-project",
  "version": "0.0.0",
  "dependencies": {
    "@langchain/mistralai": "^0.0.0",
    "langchain": "0.0.207"
  },
  "resolutions": {
    "@langchain/core": "0.1.5"
  },
  "overrides": {
    "@langchain/core": "0.1.5"
  },
  "pnpm": {
    "overrides": {
      "@langchain/core": "0.1.5"
    }
  }
}
```

The field you need depends on the package manager you're using, but we recommend adding a field for the common `yarn`, `npm`, and `pnpm` to maximize compatibility.

## Chat Models

This package contains the `ChatMistralAI` class, which is the recommended way to interface with the Mistral series of models.

To use, install the requirements, and configure your environment.

```bash
export MISTRAL_API_KEY=your-api-key
```

Then initialize

```typescript
import { ChatMistralAI } from "@langchain/mistralai";

const model = new ChatMistralAI({
  apiKey: process.env.MISTRAL_API_KEY,
  modelName: "mistral-small",
});
const response = await model.invoke(new HumanMessage("Hello world!"));
```

### Streaming

```typescript
import { ChatMistralAI } from "@langchain/mistralai";

const model = new ChatMistralAI({
  apiKey: process.env.MISTRAL_API_KEY,
  modelName: "mistral-small",
});
const response = await model.stream(new HumanMessage("Hello world!"));
```

## Embeddings

This package also adds support for Mistral's embeddings model.

```typescript
import { MistralAIEmbeddings } from "@langchain/mistralai";

const embeddings = new MistralAIEmbeddings({
  apiKey: process.env.MISTRAL_API_KEY,
});
const res = await embeddings.embedQuery("Hello world");
```

## Development

To develop the Mistral package, you'll need to follow these instructions:

### Install dependencies

```bash
yarn install
```

### Build the package

```bash
yarn build
```

Or from the repo root:

```bash
yarn build --filter=@langchain/mistralai
```

### Run tests

Test files should live within a `tests/` file in the `src/` folder. Unit tests should end in `.test.ts` and integration tests should
end in `.int.test.ts`:

```bash
$ yarn test
$ yarn test:int
```

### Lint & Format

Run the linter & formatter to ensure your code is up to standard:

```bash
yarn lint && yarn format
```

### Adding new entrypoints

If you add a new file to be exported, either import & re-export from `src/index.ts`, or add it to `scripts/create-entrypoints.js` and run `yarn build` to generate the new entrypoint.
