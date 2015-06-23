# 
<h1>fsaDragDrop</h1>
A set of directives for dragging, dropping and resizing DOM objects

<h3>Installation</h3>
<ul>
  <li>First npm install fsadragdrop</li>

  <li>add fsadragdrop into your document (note: take out the extra spaces in the script tags)
  <p>< script src="/fsadragdrop/dragdirective.js">< /script></p></li>

  <li>Next inject fsadragdrop into your project
  <p>angular.module('app', ['fsadragdrop']);</p></li>
</ul>

<h3>Usage</h3>
Now you can place any of the following attributes on any DOM object. 

<h4>fsadraggable:</h4> 
<p>Simply add 'fsadraggable' as an attribute on any element. Now that element can be dragged anywhere on the page.</p>
<p>Note: while this will work on any element, it prevents the default function of mouse dragging on that element, e.g if you stick this on a paragraph you will no longer be able to highlight that paragraph’s text.</p>

<h4>fsaresizeable:</h4>
<p>By adding 'fsaresizeable' as an attribute you will be able to resize that element. Click the right or bottom edges of the element to resize it.</p>
<p>Note: the width of the clickable border can be manually adjusted. Go into the fsaresizeable directive and modify the borderWidth variable in the fsaresizeable directive to be any value you want in pixels, the default is 10 pixels.</p>
<p>Note: While you are able to drag an element anywhere you want on the DOM, the DOM still will treat that element as if it were in its original position. E.g if you drag and resize an element, the DOM will expand as if that element were resizing where it originally was.</p>

<h4>fsacontainer:</h4>
When you add 'fsacontainer' to an element, it provides several things. 
<ul>
  <li>First it provides an element in which an fsadraggable object can be anchored to. In other words, the drag events on an fsadraggable element will also fire the drop events on an fsacontainer element.</li> 
  <li>Second it allows the transfer of data from the fsadraggable object to the fsacontainer object. To utilize the data transfer functionality, follow these steps:</li>
</ul>
  <ul>
    <li>
      Set fsadraggable and fsasetdata as attributes on the object you wish to drag.
      <p>< div fsadraggable fsasetdata>< /div></p>
    </li>
    <li>
      Set fsacontainer and fsagetdata as attributes on the object you wish to drag into.
      <p>< div fsacontainer fsagetdata>< /div></p>
    </li>
    <li>
      On the fsadraggable element, set the attribute fsasetdata equal to some scope object from the initial controller: <p>fsasetdata=”{{initialcontrollerdata}}”</p>
    </li>
    <li>
      Inject $attrs into the receiving controller: <p>app.controller('receivingController', function ($scope, $attrs) {})</p>
    </li>
    <li>
      Inside the receiving controller, set the receiving data variable equal to $attrs.fsacontainer: <p>var myReceivedData = $attrs.fsagetdata</p>
    </li>
    <li>
      <p>And that’s it! All you have to do now is drag the fsadraggable element into the fsacontainer element. You will be able to drag multiple elements to and from the container element. Each time you do, the fsagetdata attribute will be appended with a new index containing the new information. Elements can be dragged in multiple times.</p>
      <p>For example, say you had two divs: the first is a shopping list, the second is an item. You would set fsadraggable and fsasetdata on the item div, and fsacontainer and fsagetdata on the shopping list div. When you drag the item into the shopping list, the object that is on the item's controller will be transferred through the fsagetdata and fsasetdata methods. It will then become available to the shopping list controller as the 0th index on an array stored on fsagetdata. By either adding more item divs or redragging the first item into the shopping cart div, you will append more items onto the fsagetdata array.</p>
      <p>Note: that myReceivedData should be treated like an async variable. It will not be filled with data until you drag the initial object into the container object.</p>
    </li>
  </ul>
