<div align="center">
<p>
    <img
        style="width: 200px"
        width="200"
        src="https://avatars.githubusercontent.com/u/4426989?s=200&v=4"
    >
</p>
<h1>Storybook Playground</h1>

</div>

This app is created with the goals to have examples of ours React components, hooks and libraries that are created in different packages in this repository. To create the examples, in this app we are using storybook stories.

## Usage

The ideal way to run this app is from the root of the repo by executing the following command.

```bash
npm run storybook -w @nancy/playground
```

If you have already been playing with this repo, the above command is enought but if it is the first time that you are going to run this project execute the following commands from the root of the project:

```bash
fnm use
# or use your preferred node version manager to install the corresponding node version
# node version v16.13.2 check it out in .node-version from root.

npm i
npm run build
npm run storybook -w @nancy/playground
```

## Contributing

Contributions are welcome! Pull requests are welcome.

If you have a more representative example of some of the components, hooks, helpers, feel free to create a new story and create a pull request.

Read the [CONTRIBUTING guide](../../CONTRIBUTING.md) to learn about our development process, how to propose bugfixes and improvements, and how to build and test your changes to React.
