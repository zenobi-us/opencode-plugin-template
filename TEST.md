# Testing the OpenCode Plugin Generator

This document describes how to test the plugin generator.

## Manual End-to-End Test

### Prerequisites

- Bun installed
- Git configured locally (`git config user.name` and `git config user.email`)
- A test directory ready

### Test Steps

1. **Clone the template generator**

```bash
git clone https://github.com/zenobi-us/opencode-plugin-template.git test-plugin
cd test-plugin
```

2. **Run the generator**

```bash
bunx plop --plopfile ./plopfile.js
```

3. **Answer the prompts**

```
Plugin name: my-test-plugin
Plugin description: A test plugin for the opencode platform
Author name: Test Author
Author email: test@example.com
Repository URL: https://github.com/testuser/my-test-plugin
GitHub organization/username: testuser
```

### Verification Checklist

After running the generator, verify:

#### ✅ Files Generated

- [ ] `package.json` exists at root
- [ ] `src/index.ts` exists
- [ ] `README.md` exists at root
- [ ] `.github/workflows/` directory exists
- [ ] All template files are present

#### ✅ Generator Cleanup

- [ ] `template/` directory is removed
- [ ] `plopfile.js` is removed
- [ ] Old `.git/` is removed

#### ✅ Git Repository

- [ ] New `.git/` directory created
- [ ] On `main` branch: `git branch` should show `* main`
- [ ] Initial commit exists: `git log --oneline` shows initial commit
- [ ] Remote added: `git remote -v` shows origin pointing to provided URL

#### ✅ Package.json Values

```bash
# Check these match your input:
cat package.json | jq '.name'              # Should be: "my-test-plugin"
cat package.json | jq '.description'       # Should be: "A test plugin for the opencode platform"
cat package.json | jq '.author.name'       # Should be: "Test Author"
cat package.json | jq '.author.email'      # Should be: "test@example.com"
cat package.json | jq '.repository.url'    # Should be: "https://github.com/testuser/my-test-plugin"
```

#### ✅ README.md Values

```bash
# Check these are templated:
head -5 README.md                           # Should show your plugin name
grep "test@example.com" README.md           # Should find author email
grep "my-test-plugin" README.md             # Should find plugin name
```

#### ✅ Plugin Naming Conversion

Test the kebab-case conversion by running with different formats:

1. **Test CamelCase input**

   ```
   Plugin name: MyAwesomePlugin
   # Should result in: "my-awesome-plugin"
   ```

2. **Test with spaces**

   ```
   Plugin name: My Awesome Plugin
   # Should result in: "my-awesome-plugin"
   ```

3. **Test with underscores**

   ```
   Plugin name: my_awesome_plugin
   # Should result in: "my-awesome-plugin"
   ```

4. **Test with mixed case and special chars**
   ```
   Plugin name: My-Awesome_Plugin!!!
   # Should result in: "my-awesome-plugin"
   ```

#### ✅ Build & Install

```bash
# Verify the generated plugin can be set up:
bun install
mise run build
mise run lint
mise run test
```

## Automated Testing (Future)

Future testing could include:

- Unit tests for the generator prompts and filters
- Integration tests that run the generator and validate output
- Snapshot tests for generated file contents
- Script to automate the above verification checklist

Example automated test using Node:

```javascript
import fs from "fs";
import path from "path";

function validateGeneratedPlugin(outputDir) {
  const pkg = JSON.parse(
    fs.readFileSync(path.join(outputDir, "package.json"), "utf-8"),
  );
  const readme = fs.readFileSync(path.join(outputDir, "README.md"), "utf-8");

  console.assert(pkg.name === "my-test-plugin", "package.json name mismatch");
  console.assert(
    pkg.author.email === "test@example.com",
    "package.json author mismatch",
  );
  console.assert(
    readme.includes("my-test-plugin"),
    "README missing plugin name",
  );
  console.assert(
    !fs.existsSync(path.join(outputDir, "template")),
    "template dir still exists",
  );
  console.assert(
    !fs.existsSync(path.join(outputDir, "plopfile.js")),
    "plopfile still exists",
  );
}
```

## Test Results

Document your test results here:

| Date       | Tester | Plugin Name    | Result  | Notes        |
| ---------- | ------ | -------------- | ------- | ------------ |
| YYYY-MM-DD | Name   | my-test-plugin | ✅ Pass | Initial test |
