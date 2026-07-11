# npm Commands Cheat Sheet

## Project Initialization

| Command       | Purpose                                   | Example       |
| ------------- | ----------------------------------------- | ------------- |
| `npm init`    | Create a new `package.json` interactively | `npm init`    |
| `npm init -y` | Create `package.json` with default values | `npm init -y` |

---

## Package Management

| Command                    | Purpose                  | Example               |
| -------------------------- | ------------------------ | --------------------- |
| `npm install` / `npm i`    | Install all dependencies | `npm install`         |
| `npm install <package>`    | Install a package        | `npm install axios`   |
| `npm install -D <package>` | Install a dev dependency | `npm i -D typescript` |
| `npm install -g <package>` | Install globally         | `npm i -g nodemon`    |
| `npm uninstall <package>`  | Remove a package         | `npm uninstall axios` |
| `npm update`               | Update packages          | `npm update`          |
| `npm outdated`             | Show outdated packages   | `npm outdated`        |

---

## Security

| Command                 | Purpose                                        |
| ----------------------- | ---------------------------------------------- |
| `npm audit`             | Scan for vulnerabilities                       |
| `npm audit fix`         | Automatically fix vulnerabilities              |
| `npm audit fix --force` | Force updates (may introduce breaking changes) |

---

## Running Scripts

| Command         | Purpose                      |
| --------------- | ---------------------------- |
| `npm run`       | List available scripts       |
| `npm run dev`   | Run development server       |
| `npm run build` | Build project                |
| `npm run start` | Run start script             |
| `npm start`     | Shortcut for `npm run start` |
| `npm test`      | Run tests                    |

---

## Debugging & Maintenance

| Command                   | Purpose                            |
| ------------------------- | ---------------------------------- |
| `npm list`                | List installed packages            |
| `npm list --depth=0`      | Show only top-level packages       |
| `npm ls`                  | Show dependency tree               |
| `npm ls --depth=0`        | Show top-level packages            |
| `npm explain <package>`   | Explain why a package is installed |
| `npm cache verify`        | Verify npm cache                   |
| `npm cache clean --force` | Clear cache                        |
| `npm doctor`              | Check npm installation             |
| `npm rebuild`             | Rebuild native modules             |
| `npm dedupe`              | Remove duplicate packages          |
| `npm prune`               | Remove extra packages              |

---

## Package Information

| Command                | Purpose              |
| ---------------------- | -------------------- |
| `npm view <package>`   | View package details |
| `npm info <package>`   | Same as `view`       |
| `npm search <keyword>` | Search npm registry  |
| `npm show <package>`   | Show package details |

---

## Publishing

| Command             | Purpose                  |
| ------------------- | ------------------------ |
| `npm login`         | Login to npm             |
| `npm logout`        | Logout                   |
| `npm whoami`        | Current logged-in user   |
| `npm publish`       | Publish package          |
| `npm unpublish`     | Remove published package |
| `npm version patch` | Patch version            |
| `npm version minor` | Minor version            |
| `npm version major` | Major version            |

---

## Configuration

| Command                        | Purpose            |
| ------------------------------ | ------------------ |
| `npm config list`              | Show configuration |
| `npm config get <key>`         | Get config value   |
| `npm config set <key> <value>` | Set config value   |
| `npm config delete <key>`      | Delete config      |

---

## Useful Debugging Commands

| Command                   | Purpose                     |
| ------------------------- | --------------------------- |
| `npm doctor`              | Diagnose npm installation   |
| `npm cache verify`        | Verify cache                |
| `npm cache clean --force` | Clear cache                 |
| `npm explain <package>`   | Why a package exists        |
| `npm ls`                  | Dependency tree             |
| `npm ls --depth=0`        | Top-level dependencies only |

---

## Version Commands

| Command   | Purpose              |
| --------- | -------------------- |
| `npm -v`  | Show npm version     |
| `node -v` | Show Node.js version |

---

## Real-World Commands You'll Use Daily

| Situation               | Command               |
| ----------------------- | --------------------- |
| Create project          | `npm init -y`         |
| Install dependencies    | `npm install`         |
| Install one package     | `npm i axios`         |
| Install dev dependency  | `npm i -D typescript` |
| Remove package          | `npm uninstall axios` |
| Run project             | `npm run dev`         |
| Build project           | `npm run build`       |
| Run tests               | `npm test`            |
| Check outdated packages | `npm outdated`        |
| Update packages         | `npm update`          |
| Check vulnerabilities   | `npm audit`           |
| Fix vulnerabilities     | `npm audit fix`       |
| Clean install (CI/CD)   | `npm ci`              |
| Show installed packages | `npm ls --depth=0`    |
| Check npm version       | `npm -v`              |
| Check Node.js version   | `node -v`             |

---

## Top 20 Interview Commands

| No. | Command                    |
| --- | -------------------------- |
| 1   | `npm init -y`              |
| 2   | `npm install`              |
| 3   | `npm install <package>`    |
| 4   | `npm install -D <package>` |
| 5   | `npm uninstall`            |
| 6   | `npm update`               |
| 7   | `npm outdated`             |
| 8   | `npm audit`                |
| 9   | `npm audit fix`            |
| 10  | `npm ci`                   |
| 11  | `npm run`                  |
| 12  | `npm start`                |
| 13  | `npm test`                 |
| 14  | `npm ls`                   |
| 15  | `npm explain`              |
| 16  | `npm cache clean --force`  |
| 17  | `npm cache verify`         |
| 18  | `npm doctor`               |
| 19  | `npm -v`                   |
| 20  | `node -v`                  |
