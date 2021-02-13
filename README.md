# bot-my-life-back

This repo hosts the code for my website dedicated to showing the value of Robotic Process Automation (RPA) in my life. It's intended to highlight how incremental time savings can really add up. So much so that you'll find yourself recovering days of your life just by implementing a few bots.

The site was built using [Vue.js](https://vuejs.org/) and includes the [date-fn](https://date-fns.org/) javascript date library for calculating the number of business days between two dates.

As I wanted to highlight some of my work-related bots, it's important to filter out the U.S. federal holidays that occur during the work week. The 18F [us-federal-holidays](https://www.npmjs.com/package/@18f/us-federal-holidays/v/1.4.0) package is used to remove the holidays that occured during the work week (M-F) between when the bot went live and the current date.

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

### Lints and fixes files

```
npm run lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).
