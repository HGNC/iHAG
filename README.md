# iHAG - Interactive Horizontal Acyclic Grapher 

## Introduction
Draws acyclic graphs based on data within a javascript object from left to right. The graphs are interactive in that a user can click and hold on a box (node) which will highlight the path through the graph or the user can click and drag the box (node) to another area of the graph.

**For a live demo visit http://hgnc.github.io/iHAG/**

## Install
To install iHAG the easiest way would be to install [bower](http://bower.io) as described in the bower documentation and then simply run the following in your js directory:
```sh
$ bower install git://github.com/HGNC/iHAG.git
```
## Dependencies
Javascript dependencies:
- [Raphael ~2.1.4](https://github.com/DmitryBaranovskiy/raphael)

## Usage
Simply add a `<div id='YOUR-CHOICE-OF-ID'></div>` anywhere in your `<body>`.
Then at the bottom of the `<body>` add your javascript dependencies:
```html

<script type="text/javascript" src="/js/bower_components/raphael/raphael-min.js"></script>
<script type="text/javascript" src="/js/bower_components/iHAG/iHAG.js"></script>
```
Finally call the `drawHAG()` function beneth the script dependencies with a specific javascript object format:
```html
<script type="text/javascript">
  var json = [
    [
      {
        link: [
          "1"
        ],
        name: "Box A",
        id: "1"
      }
    ],
    [
      {
        link: [
          "1"
        ],
        name: "Box 1B",
        id: "2"
      },
      {
        link: [
          "1"
        ],
        name: "Box 2B",
        id: "3"
      },
    ],
    [
      {
        link: [
          "2",
          "3"
        ],
        name: "Box C",
        id: "4"
      }
    ],
    [
      {
        link: [
          "4"
        ],
        name: "Box 1D",
        id: "5"
      },
      {
        link: [
          "4"
        ],
        name: "Box 2D",
        id: "6"
      }
    ]
  ];
  $(document).ready(function(){
    drawHAG(json, {
      containerID: 'YOUR-CHOICE-OF-ID',
      targetSubjectID: 6  //choose a subject node ID
    });
  });
</script>
```
The object (`json` in the example above) that is passed to the drawHAG() function should be an array that contains an array for each
level/column in the graph. The "column" arrays hold objects that represents the nodes/boxes that are in the column. The objects contain
the following:

`name` = The node label.

`id` = A unique numerical ID that represents the node.

`link` = An array of node IDs to which the current node should link to (create an edge) in the previous column.

The node objects that would appear in the first column must have their node ID within the `link` array as though they link to themselves. The following javascript data structure produces the image of the graph below:
```javascript
var json = [
  [
    {
      link: [
        "1"
      ],
      name: "Box 1A",
      id: "1"
    },
    {
      link: [
        "10"
      ],
      name: "Box 2A",
      id: "10"
    }
  ],
  [
    {
      link: [
        "1",
        "10"
      ],
      name: "Box 1B",
      id: "2"
    },
    {
      link: [
        "1"
      ],
      name: "Box 2B",
      id: "3"
    },
  ],
  [
    {
      link: [
        "2",
        "3"
      ],
      name: "Box C",
      id: "4"
    }
  ],
  [
    {
      link: [
        "4"
      ],
      name: "Box 1D",
      id: "5"
    },
    {
      link: [
        "4"
      ],
      name: "Box 2D",
      id: "6"
    }
  ]
];
```
![iHAG example](https://cloud.githubusercontent.com/assets/9589542/11692076/c3be13fe-9e95-11e5-94df-5a36294cb499.png)
