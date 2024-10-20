# Colors

DDA is colorful game. You can use several foreground and background colors in various places:

* map data (terrain and furniture);
* item data;
* text data;
* etc.

**Note:** Map data objects can only have one color-related node defined (either `color` or `bgcolor`).

## Color string format

Whenever color is defined in JSON it should be defined in following format: `Prefix_Foreground_Background`.

`Prefix` can take one of following values:

* `c_` - default color prefix (can be omitted);
* `i_` - optional prefix which indicates that foreground color should be inverted (special rules will be applied to foreground and background colors);
* `h_` - optional prefix which indicates that foreground color should be highlighted (special rules will be applied to foreground and background colors).

`Foreground` - defines mandatory color of foreground/ink/font.

`Background` - defines optional color of background/paper.

**Note:** Not all foreground + background pairs are defined by their full name. Use in-game Color manager to see all color names.

**Note:** If color was not found by its name, then `c_unset` is used for `Foreground` and `i_white` for `Background`.

## Examples of color strings

- `c_white` - `white` color (with default prefix `c_`);
- `black` -  `black` color (default prefix `c_` is omitted);
- `i_red` - inverted `red` color;
- `dark_gray_white` - `dark_gray` foreground color with `white` background color;
- `light_gray_light_red` - `light_gray` foreground color with `light_red` background color;
- `dkgray_red` - `dark_gray` foreground color with `red` background color (deprecated prefix `dk` instead of `dark_`);
- `ltblue_red` - `light_blue` foreground color with `red` background color (deprecated prefix `lt` instead of `light_`).

## Color code

Color code is short string which defines color and can be used, for example, in maps notes.

## Possible colors

| Color (image)                                            | Color name (dda)   | Color name (curses) | Default R,G,B values | Color code | Notes                                                  |
|:--------------------------------------------------------:|:------------------:|:-------------------:|:--------------------:|:----------:|:------------------------------------------------------:|
| ![#000000](https://via.placeholder.com/20/000000/000000?text=+) | `black`            | `BLACK`             | `0,0,0`              |            |                                                        |
| ![#ff0000](https://via.placeholder.com/20/ff0000/000000?text=+) | `red`              | `RED`               | `255,0,0`            | `R`        |                                                        |
| ![#006e00](https://via.placeholder.com/20/006e00/000000?text=+) | `green`            | `GREEN`             | `0,110,0`            | `G`        |                                                        |
| ![#5c3317](https://via.placeholder.com/20/5c3317/000000?text=+) | `brown`            | `BROWN`             | `92,51,23`           | `br`       |                                                        |
| ![#0000c8](https://via.placeholder.com/20/0000c8/000000?text=+) | `blue`             | `BLUE`              | `0,0,200`            | `B`        |                                                        |
| ![#8b3a62](https://via.placeholder.com/20/8b3a62/000000?text=+) | `magenta`          | `MAGENTA`           | `139,58,98`          | `P`        |                                                        |
| ![#0096b4](https://via.placeholder.com/20/0096b4/000000?text=+) | `cyan`             | `CYAN`              | `0,150,180`          | `C`        |                                                        |
| ![#969696](https://via.placeholder.com/20/969696/000000?text=+) | `light_gray`       | `GRAY`              | `150,150,150`        | `lg`       | deprecated `lt` prefix can be used instead of `light_` |
| ![#636363](https://via.placeholder.com/20/636363/000000?text=+) | `dark_gray`        | `DGRAY`             | `99,99,99`           | `dg`       | deprecated `dk` prefix can be used instead of `dark_`  |
| ![#ff9696](https://via.placeholder.com/20/ff9696/000000?text=+) | `light_red`        | `LRED`              | `255,150,150`        |            | deprecated `lt` prefix can be used instead of `light_` |
| ![#00ff00](https://via.placeholder.com/20/00ff00/000000?text=+) | `light_green`      | `LGREEN`            | `0,255,0`            | `g`        | deprecated `lt` prefix can be used instead of `light_` |
| ![#ffff00](https://via.placeholder.com/20/ffff00/000000?text=+) | `yellow`           | `YELLOW`            | `255,255,0`          |            |                                                        |
| ![#6464ff](https://via.placeholder.com/20/6464ff/000000?text=+) | `light_blue`       | `LBLUE`             | `100,100,255`        | `b`        | deprecated `lt` prefix can be used instead of `light_` |
| ![#fe00fe](https://via.placeholder.com/20/fe00fe/000000?text=+) | `pink`             | `LMAGENTA`          | `254,0,254`          | `lm`       |                                                        |
| ![#00f0ff](https://via.placeholder.com/20/00f0ff/000000?text=+) | `light_cyan`       | `LCYAN`             | `0,240,255`          | `c`        | deprecated `lt` prefix can be used instead of `light_` |
| ![#ffffff](https://via.placeholder.com/20/ffffff/000000?text=+) | `white`            | `WHITE`             | `255,255,255`        | `W`        |                                                        |

**Note:** Default RGB values are taken from file `\data\raw\colors.json`.
**Note:** RGB values can be redefined in file `\config\base_colors.json`.

## Color rules

There are two types of special color transformation which can affect both foreground and background color:

* inversion;
* highlight.

**Note:** Color rules can be redefined (for example, `\data\raw\color_templates\no_bright_background.json`).


## Color tags

Color tags can be used in most places where strings can be displayed to the player:

```json
    "name": "[Ψ]Stop Concentrating",
    "description": "End your concentration on all of your maintained powers.\n\nChanneling this power <color_green>always succeeds</color>.",
```

```json
    "text": [
      "<color_light_blue>You see a Russian sheepdog off at the edge of your vision.  It walks past some scenery and vanishes.</color>"
    ]
```
and
```json
    { "u_message": "The <color_light_green>zombie</color> bursts in <color_red>flames!</color>", "type": "mixed" }
```

will be displayed respectively as:

![image](https://github.com/user-attachments/assets/56a68737-3265-464f-bc81-09b9fb4b8dd9)

![image](https://github.com/user-attachments/assets/eec18405-9205-4778-af13-30a3ccc7f589)

and 

![image](https://github.com/user-attachments/assets/054348a1-b4d4-4890-a72d-3dd8084516f6)


Do note how the color tags override the default color for a `"mixed"` dialogue message (`magenta`).  This is not always the case, so it requires testing to find out the intended combination.

Additionally, color tags can be combined to generate color gradients, and be nested into each other:

```json
    { "u_message": "<color_red>H</color><color_magenta>ell</color><color_red>fire</color> and brimstone." },
    { "u_message": "<color_light_gray><color_white>This text is white</color> while this text is light_gray, <color_light_red>this is light_red</color>. This is light_gray again</color>", "type": "mixed" }
```

which are displayed as:

![image](https://github.com/user-attachments/assets/fcf5589c-d8b9-47e0-a24d-6dd2441d241b)

![image](https://github.com/user-attachments/assets/4cc6d7b4-40f5-45dc-a333-951eaf486a2e)


**Note:** Items that use `relic data` automatically turn the item's displayed name in `pink`.  Color tags override this, in case one wants to "hide" it from the player, or to make them look "mundane".  Similarly, if one wants, otherwise mundane items can have colored names.

