# CSS Hexagon Tutorial by James Tauber

Here is a `100px` × `100px` `div` with a `30px` border:

    height: 100px;
    width: 100px;
    border: 30px solid #999;

## Watch what happens when each border has a different colour:

    height: 100px;
    width: 100px;
    border-top: 30px solid #C66;
    border-bottom: 30px solid #6C6;
    border-left: 30px solid #66C;
    border-right: 30px solid #CC6;

## Now if we drop the setting of `height` and explicitly set the `width` of the `div` to be `0`, we get the following:

    width: 0;
    border-top: 30px solid #C66;
    border-bottom: 30px solid #6C6;
    border-left: 30px solid #66C;
    border-right: 30px solid #CC6;

## Drop the top border and make the left and right borders `transparent` and you get this:

    width: 0;
    border-bottom: 30px solid #6C6;
    border-left: 30px solid transparent;
    border-right: 30px solid transparent;

The side borders don’t have to be the same size as the bottom border. Here’s `30px` bottom with `52px` sides:

    width: 0;
    border-bottom: 30px solid #6C6;
    border-left: 52px solid transparent;
    border-right: 52px solid transparent;

And here’s a `div` with a top border instead of a bottom border:

    width: 0;
    border-top: 30px solid #6C6;
    border-left: 52px solid transparent;
    border-right: 52px solid transparent;

Put a `104px` × `60px` `div` with a background colour between them and you get:

    width: 0;
    border-bottom: 30px solid #6C6;
    border-left: 52px solid transparent;
    border-right: 52px solid transparent;

    width: 104px;
    height: 60px;
    background-color: #6C6;

    width: 0;
    border-top: 30px solid #6C6;
    border-left: 52px solid transparent;
    border-right: 52px solid transparent;

And that’s how we get a hexagon in CSS. The 30:52 ratio in the border widths is approximately 1:√3 which is ratio required for a hexagon.

## A similar approach can be used to get a hexagon rotated 30°. We just flip around some of the directions, use `float: left` and drop the explict setting of `width` to `0`.

    float: left;
    border-right: 30px solid #6C6;
    border-top: 52px solid transparent;
    border-bottom: 52px solid transparent;

    float: left;
    width: 60px;
    height: 104px;
    background-color: #6C6;

    float: left;
    border-left: 30px solid #6C6;
    border-top: 52px solid transparent;
    border-bottom: 52px solid transparent;

## Both orientations of hexagons can easily be tiled. The first orientation involves a `margin-bottom` of `-26px` and `margin-left` of `3px` on each hexagon and a `margin-left` of `53px` on even rows:

```

.hex {
    float: left;
    margin-left: 3px;
    margin-bottom: -26px;
}
.hex .top {
    width: 0;
    border-bottom: 30px solid #6C6;
    border-left: 52px solid transparent;
    border-right: 52px solid transparent;
}
.hex .middle {
    width: 104px;
    height: 60px;
    background: #6C6;
}
.hex .bottom {
    width: 0;
    border-top: 30px solid #6C6;
    border-left: 52px solid transparent;
    border-right: 52px solid transparent;
}
.hex-row {
    clear: left;
}
.hex-row.even {
    margin-left: 53px;
}

```


## The second orientation involves a `margin-right` of `-26px` and `margin-bottom` of `-50px` on each hexagon as well as a `margin-top: 53px` on even columns:

```

.hex {
    float: left;
    margin-right: -26px;
    margin-bottom: -50px;
}
.hex .left {
    float: left;
    width: 0;
    border-right: 30px solid #6C6;
    border-top: 52px solid transparent;
    border-bottom: 52px solid transparent;
}
.hex .middle {
    float: left;
    width: 60px;
    height: 104px;
    background: #6C6;
}
.hex .right {
    float: left;
    width: 0;
    border-left: 30px solid #6C6;
    border-top: 52px solid transparent;
    border-bottom: 52px solid transparent;
}
.hex-row {
    clear: left;
}
.hex.even {
    margin-top: 53px;
}

```

And to finish things off, here’s a quick demo of a CSS 3D perspective transform applied to the hex grid:

```

\-webkit-transform: perspective(600px) rotateX(60deg);
-moz-transform: perspective(600px) rotateX(60deg);
-ms-transform: perspective(600px) rotateX(60deg);
-o-transform: perspective(600px) rotateX(60deg);
transform: perspective(600px) rotateX(60deg);
```


Addendum
--------

**Will Hardy** suggested on Twitter the following use of `:before` and `:after` to reduce the necessary `div`s to one:

```
.hex:before {
    content: " ";
    width: 0; height: 0;
    border-bottom: 30px solid #6C6;
    border-left: 52px solid transparent;
    border-right: 52px solid transparent;
    position: absolute;
    top: -30px;
}

.hex {
    margin-top: 30px;
    width: 104px;
    height: 60px;
    background-color: #6C6;
    position: relative;
}

.hex:after {
    content: "";
    width: 0;
    position: absolute;
    bottom: -30px;
    border-top: 30px solid #6C6;
    border-left: 52px solid transparent;
    border-right: 52px solid transparent;
}
```


**jawns** pointed out on Hacker News that there's a Unicode code point `U+2B22`:

⬢

<span style="color: #6C6; font-size: 135px;">&#x2B22;</span>

