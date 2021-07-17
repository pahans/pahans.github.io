---
layout: post
title: Automating React App Testing in 2021
---

Automated testing is an important part of software non-functional requirements. Manual tests **always** are expensive than automated testing. But the bitter truth is sometimes it's hard to convince people to invest in automated testing since it's a non-functional requirement.

![](/images/migrated/0__aFT__jGNhlLFafVxH.jpg)

As an engineer, there could be instances your managers force you to write code without tests to quickly get features done(so the manager can impress his bosses), and say “let's write tests later”. That later might never come until the end of the project. It’s a ticking time bomb handed over to you, off you go to [“destination fucked”](https://www.urbandictionary.com/define.php?term=Destination%20fucked). You have to work around the clock to fix issues and regressions of issues you just fixed. If the end product is fragile, no one really gives a f\*ck even if you code 16 hours a day. You might arrange war rooms, hackathons to flush the issues. But without a proper foundation, you are back to square one. Your manager even might throw you under the bus because when sh\*t hits the fan and everyone needs a scapegoat, after all, you built this app. This whole story is explained better in [“Why Agile sucks at your company — and what you can do about it”](https://laptrinhx.com/why-agile-sucks-at-your-company-and-what-you-can-do-about-it-3318998708/).

U.S. Navy Seals train with the philosophy **slow is smooth** and smooth is **fast.** Move slow enough to ensure that everything works smoothly. Not writing tests might save you time initially but in the long run, it costs a lot more it might affect your work-life balance as well because of constant [fire-fighting](https://www.techopedia.com/definition/16096/fire-fighting). Writing tests should be part of your workflow, not a painful task you always want to skip. You might have to invest a little time up-front for this. If you push this to do later, when you try to start writing tests, there will be lots of technical debt to manage because the app is not written in a testable manner.

### Testing a React App

Before we dive into React app testing I assume you are already familiar with [container components and presentational components](https://pahans.medium.com/architecting-a-react-app-in-2021-7ae278e27e6c). Here is an overview of how I think our test plan should be. I'll explain each one from bottom to top.

![](/images/migrated/1__D5V5R__do1Q__CRB24J8pgEQ.jpeg)

#### Presentational Components — Visual Tests

It’s hard to write complete tests with code for something visual. The easiest way to write tests to presentational components is visual testing with a tool like [Storybook](https://storybook.js.org/docs/riot/workflows/visual-testing) to write visual test cases and generate unit tests based on them. Storybook forces you to write better standalone components. Ability to generate unit tests based on visual tests is a real bonus. Normally, I don’t bother doing UI interaction testing at this stage. I do these in the container testing stage.

![](/images/migrated/0__zAIL__MDGEuQpTome.gif)

#### Container Components — Cypress Component Testing

For container components, the goal is to test UI interactions of components contained in the container. Those UI interactions will lead to API calls, action dispatches in the global store. The tool I am using for this is [cypress component testing](https://docs.cypress.io/guides/component-testing/introduction#What-is-Component-Testing) with \`cy.intercept()\` to mock network calls.

#### End to End Testing

In an ideal world, e2e tests are written and maintained by a team of automation engineers which is reporting to the QA team. This ensures testing of real user scenarios under the simulated environment with all components of the product. This is often the most expensive test to run. But it is still a lot cheaper than QA engineers manually testing it.

#### UI Integration Tests (I don’t really have a proper name for this.)

Let’s face it. e2e tests are expensive, time-consuming to run, pain in the ass to run locally. Stars in the galaxy need to align to pass an e2e test. e2e tests are often cover the happy path. So What I prefer is writing some e2e like tests with all APIs mocked plus tests for edge cases.

There you have it, this is how I would automate react app testing right now. Let me know what you think in the comments.