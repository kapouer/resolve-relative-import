Resolve Relative Import
=======================

A simple class to resolve es, cjs, or node modules.


Can be used with rollup, esbuild, swc, esmoduleserver, ...

Example with a rollup plugin:

```js
const Resolver = require('resolve-relative-import');

function rollupModulesPrefix(root) {
	if (!root) return;
	const Resolver = require('./resolver');
	const resolver = new Resolver({
		node_path: 'node_modules',
		prefix: root
	});
	return {
		name: "modulesPrefix",
		async resolveId(source) {
			if (!source.startsWith(root)) return null;
			const obj = resolver.resolve(source);
			return obj.path;
		}
	};
}
```


* resolver.resolve(path)
  returns a {path, url, redir} object.
  The path is a file system path.
  If redir is true, one can use url to redirect a client to the correct url.
