# YAML &rarr; Test

A simple CLI to accept a list of YAML files as an input, and converts and replaces them with test file scaffolds according to the structure of their contents.

For example, let's say you have this file:

#### Lesson.test.yaml
```yaml
- '#isOwn()'
  - when the current user is a student
    - and they are assigned the lesson
      - returns true
    - and they are not assigned the lesson
      - returns false
  - when the current user is a teacher
    - and they created the lesson
      - returns true
    - and they did not create the lesson
      - returns false
  - when the current user is not a teacher or a student
    - returns false
```

If you execute the CLI like so:

```sh
yaml-to-test ./*.test.yaml
```

It will transform that file to be this one:

#### Lesson.test.js
```js
describe('#isOwn()', () => {
  describe('when the current user is a student', () => {
    describe('and they are assigned the lesson', () => {
      it('returns true', () => {})
    })
    describe('and they are not assigned the lesson', () => {
      it('returns false', () => {})
    })
  })
  describe('when the current user is a teacher', () => {
    describe('and they created the lesson', () => {
      it('returns true', () => {})
    })
    describe('and they did not create the lesson', () => {
      it('returns false', () => {})
    })
  })
  describe('when the current user is not a teacher or a student', () => {
    it('returns false', () => {})
  })
})
```

## Features

- Recursively search through directories based on glob pattern added to CLI.
- Support both Typescript, vanilla ES6, and CoffeeScript for test generation.
- Support multiple test frameworks (Mocha, Jest, etc)
