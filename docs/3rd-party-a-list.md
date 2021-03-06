---
layout: default
title: Third party component A List
permalink: /docs/3rd-party-a-list/
---

# Third party components: the A list

Origami components may have dependencies (via Bower) on third party components.  This page documents which third party libraries are preferred where there may be multiple libraries that achieve the same goal.

<table class="o-techdocs-table">
<thead>
	<tr><th>For this</th><th>Use this</th><th>Not these</th><th>Because</th></tr>
</thead>
<tbody>
	<tr>
		<td>DOM manipulation</td>
		<td>o-dom (TBC)</td>
		<td>jQuery<br/>Mootools<br/>Dojo<br/>Prototype<br/>YUI</td>
		<td>A general purpose DOM manipulation library is invariably a common request, but large DOM libraries should be avoided since they contain numerous other features beyond simple DOM manipulation.  See also <a href="#why_not_jquery">Why not jQuery</a></td>
	</tr><tr>
		<td>AJAX</td>
		<td><a href="https://github.com/whatwg/fetch">fetch</a></td>
		<td>jQuery, superagent</td>
		<td>Components should <a href="#why_not_jquery">not use jQuery</a>, fetch is better and will be supported natively by browsers.  In the meantime a [polyfill exists](https://github.com/github/fetch) and is [available through the Polyfill Service](https://cdn.polyfill.io/).</td>
	</tr><tr>
		<td>Event delegation</td>
		<td><a href="https://github.com/ftlabs/ftdomdelegate">ftdomdelegate</a></td>
		<td>jQuery</td>
		<td>Components should <a href="#why_not_jquery">not use jQuery</a>.</td>
	</tr><tr>
		<td>JavaScript utils</td>
		<td><a href="https://github.com/lodash/lodash-node">Lodash-node</a></td>
		<td>Underscore, Lodash</td>
		<td>Lodash is roughly functionally equivalent to Underscore, but generally delivers faster performance, and includes some useful things not available in Underscore. Lodash-node has the additional benefit of making each method individually requireable (the 'modern' version of its methods are preferred) e.g. `require('lodash-node/modern/functions/throttle')`</td>
	</tr><tr>
		<td>Template engine</td>
		<td><a href="https://github.com/twitter/hogan.js">Hogan</a></td>
		<td>Mustache<br/>Handlebars</td>
		<td>
			<p>It's compatible with Mustache templates, but offers additional features on top of Mustache's syntax. Origami has no opinion on how product developers should build applications, so when a component's purpose is to offer a raw template to the developer, it must use only fully Mustache-compatible syntax (but these components would also not actually require the template engine themselves).</p>
			<p>Components that contain templates but only use them internally in order to render a UI element, may use the more advanced template syntax offered by Hogan, and prefer Hogan as the template engine.</p>
		</td>
	</tr><tr>
		<td>Touch interactions</td>
		<td><a href="http://hammerjs.github.io/">Hammer.JS</a></td>
		<td></td>
		<td>
			<p>It offers a highly extensible, well tested and lightweight way to interact with touch events, including both single- and multi-touch gestures.</p>
		</td>
	</tr>
</tbody>
</table>


## Why not Modernizr?

Components are required to not do anything in global scope, which rules out invoking Modernizr directly.  Components wishing to use a new browser feature should simply declare it as a requirement in the browserFeatures section of `origami.json`.  A product developer can then choose to either load the module only if the required feature is present, or polyfill it to ensure that it is.


## Why not jQuery?

jQuery is a commonly requested general purpose library, and may well already be on a product page due to use in the product or demands from advertisers.  However, component authors *should* [avoid](http://youmightnotneedjquery.com/) using jQuery.  As a whole, jQuery is an example of a [god object](http://en.wikipedia.org/wiki/God_object) which poses problems for smooth upgrading of component dependencies (it's much easier to update things if they have smaller APIs and fewer dependents).

There are also specific modules within jQuery that don't operate in an optimal way:

* **Events**: jQuery's event system is great, but it includes a proprietary namespacing strategy which isn't consistent with the way Origami namespacing normally works.  Instead, use [ftdomdelegate](https://github.com/ftlabs/ftdomdelegate), which provides the same familiar `on` and `off` methods.
* **Promises**: jQuery lacks promises but does have Deferred, which can achieve similar ends but is not compatible with the standards-based promise.  Instead, use [native promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), and declare `promises` as a requirement for your module in the `browserFeatures` property of `origami.json`.
* **Data**: jQuery provides the ability to store arbitrary data against DOM elements outside of the scope of your JavaScript module, which is a practice we would like to avoid.
