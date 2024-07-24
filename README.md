# Professional README Generator

![License](https://img.shields.io/badge/License-MIT-blue.svg)

## Description

The Professional README Generator is a command-line application that dynamically generates a high-quality README file for your project. By answering a series of prompts, you can create a professional README file with sections like Description, Installation, Usage, License, Contributing, Tests, and Questions.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [License](#license)
- [Contributing](#contributing)
- [Tests](#tests)
- [Questions](#questions)
- [Tutorial Video](#tutorial-video)

## Installation

To install the necessary dependencies, run the following command:

```sh
npm install
```

## Usage

To use the application, run the following command:

```sh
node index.js
```

You will be prompted to enter the following information:
- Project title
- Description of the project
- Installation instructions
- Usage information
- Contribution guidelines
- Test instructions
- Choose a license for your project
- GitHub username
- Email address

Once you provide the information, a `README.md` file will be generated in the root directory of your project.

## License

This project is licensed under the MIT license.

## Contributing

Please feel free to reach out contribute.

## Tests

To run tests, run the following command:

```sh
npm test
```

## Questions

If you have any questions about the project, please contact me at [bjorntimothyjohansson@gmail.com](mailto:bjorntimothyjohansson@gmail.com). You can find more of my work at [Bbbjrn](https://github.com/Bbbjrn).

## Tutorial Video

A walkthrough video demonstrating the functionality of the application can be found [here](link-to-video).

---

### Project Structure

Here is an overview of the key files in the project:

#### `index.ts`

```typescript
import inquirer from 'inquirer';
import fs from 'fs';
import generateMarkdown from "./utils/generateMarkdown.js";

const questions = [
    {
        type: 'input',
        name: 'title',
        message: 'What is the title of your project?',
    },
    {
        type: 'input',
        name: 'description',
        message: 'Please provide a description of your project',
    },
    {
        type: 'input',
        name: 'installation',
        message: 'Please provide installation instructions for your project',
    },
    {
        type: 'input',
        name: 'usage',
        message: 'Please provide usage information for your project',
    },
    {
        type: 'list',
        name: 'license',
        message: 'Please choose a license for your project',
        choices: ['MIT', 'Apache', 'GPL', 'BSD', 'None'],
    },
    {
        type: 'input',
        name: 'contributing',
        message: 'Please provide contribution guidelines for your project',
    },
    {
        type: 'input',
        name: 'tests',
        message: 'Please provide test instructions for your project',
    },
    {
        type: 'input',
        name: 'github',
        message: 'What is your GitHub username?',
    },
    {
        type: 'input',
        name: 'email',
        message: 'What is your email address?',
    },
];

function writeToFile(fileName: string, data: string): void {
    fs.writeFile(fileName, data, (err) =>
        err ? console.error(err) : console.log('Success!')
    );
}

function init(): void {
    inquirer.prompt(questions)
    .then((responses) => {
        const markdown = generateMarkdown(responses);
        writeToFile('README.md', markdown);
    });    
}

init();
```

#### `generateMarkdown.ts`

```typescript
function renderLicenseBadge(license: string): string {
  if (license === 'None') {
    return '';
  }
  return `![License](https://img.shields.io/badge/license-${license}-blue.svg)`;
}

function renderLicenseLink(license: string): string {
  if (license === 'None') {
    return '';
  }
  return `\n* [License](#license)\n`;
}

function renderLicenseSection(license: string): string {
  if (license === 'None') {
    return '';
  }
  return `## License

This project is licensed under the ${license} license.`;
}

function generateMarkdown(data: {
  title: string;
  description: string;
  installation: string;
  usage: string;
  contributing: string;
  tests: string;
  license: string;
  github: string;
  email: string;
}): string {
  return `# ${data.title}

${renderLicenseBadge(data.license)}

## Description

${data.description}

## Table of Contents

* [Installation](#installation)
* [Usage](#usage)
* [Contributing](#contributing)
* [Tests](#tests)
* [Questions](#questions)
${renderLicenseLink(data.license)}

## Installation

${data.installation}

## Usage

${data.usage}

## Contributing

${data.contributing}

## Tests

${data.tests}

${renderLicenseSection(data.license)}

## Questions

For any questions, please contact me with the information below:

GitHub: [${data.github}](https://github.com/${data.github})

Email: ${data.email}
`;
}

export default generateMarkdown;
```

### Additional Information

- **Dependencies**:
  - `inquirer` is used for prompting user inputs.
  - `fs` is used for file system operations.

- **License**:
  This project is licensed under the MIT license. See the [LICENSE](LICENSE) file for details.

By following these instructions, you can easily generate a professional README file for your project. If you encounter any issues or have questions, feel free to reach out via GitHub or email.

### Tutorial Video

A walkthrough video demonstrating the functionality of the application can be found [here](./assets/Module07-challenge.mov).