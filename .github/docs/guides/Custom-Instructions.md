# Repository Custom Instructions for Copilot

Repository custom instructions let you provide Copilot with repository-specific guidance and preferences.

Prerequisites for repository custom instructions
You must have a custom instructions file (see the instructions below).
Custom instructions must be enabled. This feature is enabled by default. See Enabling or disabling repository custom instructions later in this article.
Creating custom instructions
VS Code supports two types of repository custom instructions:

Repository-wide custom instructions, which apply to all requests made in the context of a repository.

These are specified in a copilot-instructions.md file in the .github directory of the repository. See Creating repository-wide custom instructions.

Path-specific custom instructions, which apply to requests made in the context of files that match a specified path.

These are specified in one or more NAME.instructions.md files within the .github/instructions directory in the repository. See Creating path-specific custom instructions.

If the path you specify matches a file that Copilot is working on, and a repository-wide custom instructions file also exists, then the instructions from both files are used.

Creating repository-wide custom instructions
In the root of your repository, create a file named .github/copilot-instructions.md.

Create the .github directory if it does not already exist.

Add natural language instructions to the file, in Markdown format.

Whitespace between instructions is ignored, so the instructions can be written as a single paragraph, each on a new line, or separated by blank lines for legibility.

Creating path-specific custom instructions
Create the .github/instructions directory if it does not already exist.

Create one or more NAME.instructions.md files, where NAME indicates the purpose of the instructions. The file name must end with .instructions.md.

At the start of the file, create a frontmatter block containing the applyTo keyword. Use glob syntax to specify what files or directories the instructions apply to.

For example:

---
applyTo: "app/models/**/*.rb"
---
You can specify multiple patterns by separating them with commas. For example, to apply the instructions to all TypeScript files in the repository, you could use the following frontmatter block:

---
applyTo: "**/*.ts,**/*.tsx"
---
To apply the instructions to all files, use applyTo: "**".

Add your custom instructions in natural language, using Markdown format. Whitespace between instructions is ignored, so the instructions can be written as a single paragraph, each on a new line, or separated by blank lines for legibility.

Did you successfully add a custom instructions file to your repository?

 

Writing effective repository custom instructions
The instructions you add to your custom instruction file(s) should be short, self-contained statements that provide Copilot with relevant information to help it work in this repository. Because the instructions are sent with every chat message, they should be broadly applicable to most requests you will make in the context of the repository.

The exact structure you utilize for your instructions file(s) will vary by project and need, but the following guidelines provide a good starting point:

Provide an overview of the project you're working on, including its purpose, goals, and any relevant background information.
Include the folder structure of the repository, including any important directories or files that are relevant to the project.
Specify the coding standards and conventions that should be followed, such as naming conventions, formatting rules, and best practices.
Include any specific tools, libraries, or frameworks that are used in the project, along with any relevant version numbers or configurations.
The following instructions file(s) is an example of these practices in action:

# Project Overview

This project is a web application that allows users to manage their tasks and to-do lists. It is built using React and Node.js, and uses MongoDB for data storage.

## Folder Structure

- `/src`: Contains the source code for the frontend.
- `/server`: Contains the source code for the Node.js backend.
- `/docs`: Contains documentation for the project, including API specifications and user guides.

## Libraries and Frameworks

- React and Tailwind CSS for the frontend.
- Node.js and Express for the backend.
- MongoDB for data storage.

## Coding Standards

- Use semicolons at the end of each statement.
- Use single quotes for strings.
- Use function based components in React.
- Use arrow functions for callbacks.

## UI guidelines

- A toggle is provided to switch between light and dark mode.
- Application should have a modern and clean design.
You should also consider the size and complexity of your repository. The following types of instructions may work for a small repository with only a few contributors, but for a large and diverse repository, these may cause problems:

Requests to refer to external resources when formulating a response
Instructions to answer in a particular style
Requests to always respond with a certain level of detail
For example, the following instructions may not have the intended results:

Always conform to the coding styles defined in styleguide.md in repo my-org/my-repo when generating code.

Use @terminal when answering questions about Git.

Answer all questions in the style of a friendly colleague, using informal language.

Answer all questions in less than 1000 characters, and words of no more than 12 characters.
Repository custom instructions in use
The instructions in the file(s) are available for use by Copilot Chat as soon as you save the file(s). The complete set of instructions will be automatically added to requests that you submit to Copilot in the context of that repository. For example, they are added to the prompt you submit to Copilot Chat.

Custom instructions are not visible in the Chat view or inline chat, but you can verify that they are being used by Copilot by looking at the References list of a response in the Chat view. If custom instructions were added to the prompt that was sent to the model, the .github/copilot-instructions.md file is listed as a reference. You can click the reference to open the file.

Screenshot of an expanded References list, showing the 'copilot-instructions.md' file highlighted with a dark orange outline.

Enabling or disabling repository custom instructions
You can choose whether or not you want Copilot to use repository-based custom instructions.

Enabling or disabling custom instructions for Copilot Chat
Custom instructions are enabled for Copilot Chat by default but you can disable, or re-enable, them at any time. This applies to your own use of Copilot Chat and does not affect other users.

Open the Setting editor by using the keyboard shortcut Command+, (Mac) / Ctrl+, (Linux/Windows).
Type instruction file in the search box.
Select or clear the checkbox under Code Generation: Use Instruction Files.
Enabling or disabling custom instructions for Copilot code review
Custom instructions are enabled for Copilot code review by default but you can disable, or re-enable, them in the repository settings on GitHub.com. This applies to Copilot's use of custom instructions for all code reviews it performs in this repository.

On GitHub, navigate to the main page of the repository.

Under your repository name, click  Settings. If you cannot see the "Settings" tab, select the  dropdown menu, then click Settings.

Screenshot of a repository header showing the tabs. The "Settings" tab is highlighted by a dark orange outline.
In the "Code & automation" section of the sidebar, click  Copilot, then Code review.

Toggle the “Use custom instructions when reviewing pull requests” option on or off.

Enabling and using prompt files
Note

Copilot prompt files are in public preview and subject to change. Prompt files are only available in VS Code. See About customizing GitHub Copilot Chat responses.
For community-contributed examples of prompt files for specific languages and scenarios, see the Awesome GitHub Copilot Customizations repository.
Prompt files let you build and share reusable prompt instructions with additional context. A prompt file is a Markdown file, stored in your workspace, that mimics the existing format of writing prompts in Copilot Chat (for example, Rewrite #file:x.ts). You can have multiple prompt files in your workspace, each of which defines a prompt for a different purpose.

Enabling prompt files
To enable prompt files, configure the workspace settings.

Open the command palette by pressing Ctrl+Shift+P (Windows/Linux) / Command+Shift+P (Mac).
Type "Open Workspace Settings (JSON)" and select the option that's displayed.
In the settings.json file, add "chat.promptFiles": true to enable the .github/prompts folder as the location for prompt files. This folder will be created if it does not already exist.
Creating prompt files
Open the command palette by pressing Ctrl+Shift+P (Windows/Linux) / Command+Shift+P (Mac).

Type "prompt" and select Chat: Create Prompt.

Enter a name for the prompt file, excluding the .prompt.md file name extension. The name can contain alphanumeric characters and spaces and should describe the purpose of the prompt information the file will contain.

Write the prompt instructions, using Markdown formatting.

You can reference other files in the workspace by using Markdown links—for example, [index](../../web/index.ts)—or by using the #file:../../web/index.ts syntax. Paths are relative to the prompt file. Referencing other files allows you to provide additional context, such as API specifications or product documentation.

Using prompt files
At the bottom of the Copilot Chat view, click the Attach context icon ().

In the dropdown menu, click Prompt... and choose the prompt file you want to use.

Optionally, attach additional files, including prompt files, to provide more context.

Optionally, type additional information in the chat prompt box.

Whether you need to do this or not depends on the contents of the prompt you are using.

Submit the chat prompt.

For more information about prompt files, see Custom instructions for GitHub Copilot in VS Code in the Visual Studio Code documentation.