# TestNodeApp - GitHub Actions with Containers

![Node.js](https://img.shields.io/badge/Node.js-16-green)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-blue)
![Docker](https://img.shields.io/badge/Container-node:16-blue)

## 📋 Description

This repository demonstrates the implementation of **GitHub Actions with Docker containers** to run CI/CD pipelines. The project uses a simple Node.js application that employs the `moment` library to illustrate how to configure automated workflows running inside containers.

## 🎯 Objective

The main objective is to demonstrate:

- ✅ GitHub Actions configuration with Docker containers
- ✅ Node.js application execution in containerized environments
- ✅ Dependency management in CI/CD pipelines
- ✅ Automated testing and validation on every push

## 🏗️ Project Structure

```
TestNodeApp/
├── .github/
│   └── workflows/
│       └── build.yml          # GitHub Actions workflow
├── node_modules/              # Dependencies (generated)
├── app.js                     # Main application
├── package-lock.json          # Dependencies lock file
├── package.json               # Project configuration
└── README.md                  # This file
```

## 📦 Application (app.js)

The Node.js application performs basic operations:

```javascript
const moment = require('moment');
let i = 5;
let j = 10;
console.log("Starting...");
console.log('The sum is: ' + (5+10));

let date = moment().format('LL');
console.log('And the date is: ' + date);
```

**Features:**
- Sum of two numbers
- Current date formatting using `moment.js`
- Demonstration of npm dependencies usage

## ⚙️ GitHub Actions Workflow

### File: `.github/workflows/build.yml`

```yaml
on: push
jobs:
  build-node:
    runs-on: ubuntu-latest
    container: node:16
    steps:
      - run: echo "TESTING"
      - run: node --version
      - run: npm --version
      - uses: actions/checkout@v3
      - run: npm install
      - run: node app.js
```

### 🔍 Workflow Explanation

| Step | Command | Description |
|------|---------|-------------|
| **1** | `echo "TESTING"` | Prints startup message |
| **2** | `node --version` | Checks Node.js version |
| **3** | `npm --version` | Checks npm version |
| **4** | `actions/checkout@v3` | Clones the repository |
| **5** | `npm install` | ⚠️ **CRITICAL**: Installs dependencies |
| **6** | `node app.js` | Runs the application |

### 🐳 Container Features

- **Base image**: `node:16`
- **Runner**: `ubuntu-latest`
- **Trigger**: Runs on every `push`

## ⚠️ Common Problem and Solution

### Error: `MODULE_NOT_FOUND`

```bash
Error: Cannot find module 'moment'
code: 'MODULE_NOT_FOUND'
```

**Cause**: Dependencies were not installed before running the application.

**Solution**: Ensure `npm install` is included in the workflow before `node app.js`.

## 🚀 How to Use This Repository

### 1. Clone the repository
```bash
git clone https://github.com/your-username/TestNodeApp.git
cd TestNodeApp
```

### 2. Install dependencies locally
```bash
npm install
```

### 3. Run the application
```bash
node app.js
```

### 4. Push to trigger GitHub Actions
```bash
git add .
git commit -m "Test GitHub Actions"
git push origin main
```

## 📊 Dependencies

```json
{
  "dependencies": {
    "moment": "^2.29.x"
  }
}
```

## 🔑 Key Concepts

### GitHub Actions with Containers

1. **Isolation**: Each job runs in a clean container
2. **Reproducibility**: Same environment on every execution
3. **Portability**: Works the same locally and in the cloud
4. **Scalability**: Easy to replicate and modify

### Advantages of Using Containers

- ✅ Consistent and predictable environment
- ✅ Doesn't contaminate host system
- ✅ Easy Node.js version switching
- ✅ Better system dependency management

## 📝 Important Notes

- The container is destroyed after each execution
- Dependencies must be installed on each run
- Generated files don't persist between executions
- Source code is obtained via `actions/checkout`

## 🎓 Learning Outcomes

This project teaches:

1. Basic GitHub Actions configuration
2. Container usage in workflows
3. Dependency management in CI/CD
4. Debugging common pipeline errors
5. Best practices for automation

## 🤝 Contributing

Contributions are welcome. Please:

1. Fork the project
2. Create a branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -m 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Open a Pull Request

## 📄 License

This project is open source and available for educational purposes.

---

**Developed for educational purposes to demonstrate GitHub Actions with containers** 🚀

---

## 🌐 Translations

📖 **[Read this in Spanish (Leer en Español)](./README_es.md)**