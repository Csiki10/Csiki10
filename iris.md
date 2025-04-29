
An idea / guide for the new IRIS client design system implementation based on 
[Figma](https://www.figma.com/design/WcmQXqURiNGlAAyvYuo1jo/IRIS?node-id=0-1&node-type=canvas&t=cTsas0iIUYH9LOuC-0)

Track [3rd party components](https://github.com/DamitDev/iris/wiki/IRIS-Client-3rd-party-components---services)

## 🎨 Figma

[Figma](https://www.figma.com/design/WcmQXqURiNGlAAyvYuo1jo/IRIS?node-id=0-1&node-type=canvas&t=cTsas0iIUYH9LOuC-0) 

PW: irisAking
- use **figma dev mode** during development (request accces from Dorn András)
- use `rem `as unit instead of px
- use `css-tailwind-codegen` extension for auto class translation (add this in extensions panel in figma)

## 🧪 Technologies
- [Tailwind 2.2.19](https://v2.tailwindcss.com/docs)
- [Font Awsome 5.15.4](https://fontawesome.com/icons) icons & [Ember Fontawesome](https://github.com/FortAwesome/ember-fontawesome) icons
- [Ember.js](https://guides.emberjs.com/v5.12.0/) --> new things should be written in .ts
- [clsx](https://www.npmjs.com/package/clsx)
- [cva](https://cva.style/docs)

## 🛠 Implementation approach
### 🕺🏽 Styling & CSS
- Tailwind css styling prefered over calssic css
- old / not used css classes should be removed during development and slowly deleting all individual not needed .css files
- if css usage required, add a new `sytles/ui/component-name.css` file under the `styles/ui` folder
- design tokens/variables for colours, spacing, sizing etc are placed in `tw.css` class
- for colors use hsla variable and in `tailwind.config` add a fallback value as well
- in the `tailwind.config` file these `tw.css` variables are used for style extending
- In the future cosnider moving from extende to override to prevent any other not design style aplly
- Dont use @apply in css files if can [blog](https://blog.fossnsbm.org/5-tailwind-css-best-practices-for-preventing-a-css-nightmare-c1602b3f8120)

- place complex css logic into .ts file under getter and use `cva` or `clsx` for better usage
- smaller logic required css can be palced in template like `'{{if @disabled "opacity-40"}} ...'`

### 🏗️ Components
- new Ui components should be placed under `components/ui` using .ts
- try grouping similar ones to keep the size minimal
- command for glimmer compoennt genration: `ember generate component ui/example --pod`
- add short jsdoc to the input params interface, abobe each prop
- add usage example above the component class
- write a short description about what the component does and if it has any unusuall or worth to mention extra feature
- place a link for 3rd party doc if its an extension
- define return param type if known
- add newly founded and in use [3rd party components](https://github.com/DamitDev/iris/wiki/IRIS-Client-3rd-party-components---services) into the list 
- for icons only use Ember Icons `<FaIcon @icon={{user}}>`

### 🅰️ Naming conventions
- keep the naming convention that the generator make
- use the onClick, onChange, onSelect prop input name
- use handleClick, handleChange, handleSelect method name in component and add extra logic if needed before calling passed-in method

### 🔐 Type definitions
under the project `root/types` folder, add a type definition for own services components and any other thing that needs
|File / Folder|Description  |
|-------------|------------------|
|     types/services/        | service type defs|
|     types/services        | service registry |
|     types/components| 3rd party components registry|
|     types/global| 3rd party components def & other defs & registry |

### 🛤️ Branching strategy
- the main branch called [#2922-iris-v2](https://github.com/DamitDev/iris/issues/2922) serves as a second master
- in the issue description add any related comment eg. component to delete after replacing all of them to new ones ans so on
- this branch state is up to date with the actual master by rebasing it after releases
- everny new branch should start from this v2 with a convention `ui/#[issue-number][description]`
- thre is a `container-#2922-iris-v2` that serves as an UAT for testing
- after finished developing make a PR-to the v2 and after a finished page it can be released to the container

### 👷 Run project & Start Developing
1. `git fecth iris` to get the remote braches
1. `git checkout -b "#2922-iris-v2"` to stand on the new master
1. `git pull --rebase` to get the latest state
1. `yarn install` to get needed packages
1. `git checkout -b "ui/#[issue-number][description]"` to start a new branch

### 📌 Best Practices & Principles
- [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
- [KISS](https://en.wikipedia.org/wiki/KISS_principle)
- [Open-closed (do not over abstract )](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle) 

[**Youtube videos**](https://www.youtube.com/watch?v=cZc4Jn5nK3k&list=PL3hJVrWcsF5uJZFecunCl7NuMnqXgmCdj)
