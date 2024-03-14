## Installation and Setup

1. **Installing Angular CLI**: Use npm to install Angular CLI globally: `npm install -g @angular/cli` (Consider using `npx` to avoid having a global version).

2. **Angular Workspace Creation**:
   - To create a new Angular workspace without a default application: `ng new appName --createApplication=false`.
   - Alternatively, simply run: `ng new appName`.

3. **Workspace Walkthrough**:
   - `tsconfig.spec.json`: Responsible for compiling spec.ts files (all the unit tests end in spec.ts).
   - `tsconfig.app.json`: Compiles the user code, i.e., all the .ts files.
   - `package.json` and `package-lock.json`: Dependency management files.
   - `karma.conf.js`: Configuration file to run tests generated by the user using Jasmine.
   - `angular.json`: Contains all the information related to the current workspace.
   - `.gitignore`
   - `.editorconfig`
   - `.browserslistrc`: his file has all the browsers our app supports or browser user wants his application to support  I) inside the src folder we will write all our code.
   - `src` folder: Contains all the user code.

4. **Monorepo**:
   In Angular development, a monorepo refers to a single repository containing multiple projects or applications. This approach streamlines version control, dependency management, and code sharing across projects. Within a monorepo, each Angular application or library resides in its own directory, allowing for centralized configuration and easier collaboration among developers. 

5. **Inside the src Folder**:
   - `test.ts`: Used by Karma.
   - `.css` file: For global styling.
   - `polyfills.ts`: Plays a critical role in ensuring cross-browser compatibility by providing polyfills for features not supported by all browsers.
   - `main.ts`: Serves as the starting point for an Angular application.
   - `index.html`: Main file which will be rendered.
   - `environments` folder.
   - `assets` folder.
   - `app` folder.

6. **Inline HTML and CSS**:
   - Inline HTML and CSS can be written using the template and style properties:
   ```typescript
      @Component({
        selector: 'app-example',
        template: `<p>This is an example component with inline HTML</p>`,
        styles: [`p { color: blue; }`]
      })
      export class ExampleComponent {}
7. **Components**:
   - Views that will be rendered by the browser.
     ```typescript
        ng g c componentName
