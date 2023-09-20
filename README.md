# Dev Notes

This is a repository of guides, tutorials, code snippets, and general notes
for various types of software development.

The intended audience is mostly my forgetful self, however, if others stumble
upon this repository and find it useful, then all the better!

## TODO

1. Add notes on using Jekyll
   1. Using webpack and React with Jekyll (https://medium.com/@allizadrozny/using-webpack-and-react-with-jekyll-cfe137f8a2cc)
   1. Using React, Webpack, and Babel (https://dev.to/shivampawar/setup-webpack-and-babel-for-a-react-js-application-24f5, also see https://github.com/Pathos-Design-Studio/pathos-site/commit/6ea66b3dd0b0f68c6890164483d4566c5556d6a3)
   1. Using Flow, ESLint, and Prettier (https://flow.org/en/docs/install/, https://flow.org/en/docs/tools/eslint/, option 2 here: https://stackoverflow.com/questions/51563112/flow-throws-error-cannot-resolve-module-react-redux-even-tho-its-installed, and impl here https://github.com/Pathos-Design-Studio/pathos-site/commit/954b0c235c0cab5e06737c80d427722bc80991de)
   1. Integrating Strapi with Jekyll (https://strapi.io/blog/building-a-static-website-using-jekyll-and-strapi)
1. Add notes on using React
   1. Add notes on using React with strapi (https://docs.strapi.io/dev-docs/integrations/react)
1. Add UX implementation notes
   1. CSS notes - [Mozilla Guide](https://developer.mozilla.org/en-US/docs/Learn/CSS)
      1. Popular CSS frameworks
      2. Critical concepts: css selectors, cascade/specificity/inheritance, box-model, flexbox/grids/floats/positioning
      3. Implementing accessibility guidelines
1. Add Rails notes top section
   1. Generating a new app
   1. Generating tests and testing
1. Add CI/CD notes - Jenkins
1. Add DevOps notes on deploying Rails
   1. How to [deploy in production mode](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_Ruby.container.html) to
      reduce source bundle size and memory footprint (make sure to add
      RAILS_ENV to production and update RACK_ENV to deployment)
   1. How to add pre-commit hooks (esp. testing hooks) - [pre-commit repo](https://github.com/jish/pre-commit), [pre-commit ci docs](https://jish.github.io/pre-commit/checks/ci/)
1. Add notes on Python gotchyas
   1. Writing [packages](https://docs.python.org/3/tutorial/modules.html#packages)
   1. Relative vs. absolute imports and directory context switching (note: always use absolute) -- [see stackoverflow](https://stackoverflow.com/questions/14132789/relative-imports-for-the-billionth-time)
   1. Updating virtual env to [point to your local packages](https://stackoverflow.com/questions/4757178/how-do-you-set-your-pythonpath-in-an-already-created-virtualenv/47184788#47184788) so they're in the python path
1. Add visual & UX design notes
   1. Import old notes & resources - [UX Design Cheatsheet](https://docs.google.com/document/d/1EM650-Spqyc-uiUeUZf2txY1c_74QC-SmctJwg2Nhi4/edit#)
   1. Watch figma videos and write out important highlights - [Visual Design](https://www.youtube.com/playlist?list=PLlJddLya2kqngHEHAEumTC7IP5dBJyq23), [UX Design](https://www.youtube.com/playlist?list=PLlJddLya2kqlIrrgpO8odTK-awv-jZ0of)
