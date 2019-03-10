# Must Haves on a Project

This is just a guide to what every project _should_ have.

### Package.json
Package.json is a very important files responsable to tell us what are our project _dependencies_ and _version_

You can start with `npm init` then follow the instructions.

For more: [npmjs](https://docs.npmjs.com)

### .gitignore
*.gitignore* is extremely usefull to tell `Git` what from our folder must go to repository. There is a lot of times where your repository has folders which you dont need them to go to your repository, then, u use _.gitignore_

You can start using [gitignore npm package](https://www.npmjs.com/package/gitignore).

`npm i gitignore -g`

use `gitignore -types` to see a list of all typex. <br>
Ex.: `gitignore Node` simple like that.

### Documentation
#### Readme
Core description of your repository. Apresentation, How to use, Best pratices and etc... 

You can use the [Awesome-readme repository](https://github.com/matiassingers/awesome-readme) to get some instructions when building your doc.

Ex.: [Willian Justen Proj Documentation](https://github.com/lyef/lyef-react-component), [Template](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)

#### License
[Popular licenses](https://opensource.org/licenses)

#### Contributing
Instructions on how contribute on your project
[Example](https://github.com/lyef/lyef-react-component/blob/master/CONTRIBUTING.md)

### Styleguide
Is a documentation of pattern your code must follow, exist multiples styleguides, like:

- [Airbnb styleguide](https://github.com/airbnb/javascript)
- [Standard styleguide](https://github.com/standard/standard)

Combine your styleguide with ESLint

### ESLint
Eslint will pass trought your files and chech if they are following the styleguide you setted.

starting with `npm i eslint --save-dev` then `eslint --init` to start your project.

### EditorConfig
...
### NPM Scripts
...
### Git Hooks (husky)
...

## Project quality
### Common sense
Think before creating something, like:
- Verify variables names
- Verify if is your code legible, anyone can understand what u doing?
- Think before and analyse after

### Semantic variables
- Use semantic names, variable for a user, use `user`, `userData`, something usefull, not *a* or *b*
- Simples words, semantic, not a phrase, easy to write and read
- Use verbs as variables, `getUser`, `getProduct`, `deleteProduct`

### Methods
- Methods must be short, if is it to long, divide it
- Has only one responsability, do one thing
- Re-usable method, dynamic

### Dont comment everything on your code
A good code is the on that without comments you can understand everything it must do.

### Think a lot about the project
If u dont worry about your project, how thing gonna run, how your team will do it, you will throw against techinique debts

### TESTS!
Fundamental to garantee quality of your project