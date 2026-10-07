# Example Gallery

This gallery contains a collection of code snippets together with their corresponding output, illustrating different colors themes in Manim and example objects.


```{eval-rst}
.. manim:: NumberPlaneExample
    :save_last_frame:
    
    
    import manim as m

    from manim_themes.manim_theme import apply_theme
    
    class NumberPlaneExample(m.Scene):
    
        def setup(self):
            # Set the background color to a light beige
            theme = "Obsidian"
            apply_theme(manim_scene=self, theme_name=theme)
    
    
    
        def construct(self):
            dot = m.Dot(m.ORIGIN)
            arrow = m.Arrow(m.ORIGIN, [2, 2, 0], buff=0)
    
    
            numberplane = m.NumberPlane()
            origin_text = m.Text('(0, 0)').next_to(dot, m.DOWN)
            tip_text = m.Text('(2, 2)').next_to(arrow.get_end(), m.RIGHT)
            self.add(numberplane, dot, arrow, origin_text, tip_text)
    
    
    if __name__ == '__main__':
        import os
        from pathlib import Path
    
        FLAGS = "-pqm"
        SCENE = "AxesExample"
    
        file_path = Path(__file__).resolve()
        os.system(f"manim {Path(__file__).resolve()} {SCENE} {FLAGS}")


```


```{eval-rst}
.. manim:: PolygonExample
    
    
    import manim as m
    import numpy as np
    
    from manim_themes.manim_theme import apply_theme
    
    class PolygonExample(m.Scene):
    
        def setup(self):
            # Set the background color to a light beige
            #theme = "Retro"
            theme="Crayon Pony Fish"
            apply_theme(manim_scene=self, theme_name=theme)
    
    
    
        def get_rectangle_corners(self, bottom_left, top_right):
            return [
                (top_right[0], top_right[1]),
                (bottom_left[0], top_right[1]),
                (bottom_left[0], bottom_left[1]),
                (top_right[0], bottom_left[1]),
            ]
    
        def construct(self):
            ax = m.Axes(
                x_range=[0, 10],
                y_range=[0, 10],
                x_length=6,
                y_length=6,
                axis_config={"include_tip": False},
            )
    
            t = m.ValueTracker(5)
            k = 25
    
            graph = ax.plot(
                lambda x: k / x,
                color=m.YELLOW_D,
                x_range=[k / 10, 10.0, 0.01],
                use_smoothing=False,
            )
    
            def get_rectangle():
                polygon = m.Polygon(
                    *[
                        ax.c2p(*i)
                        for i in self.get_rectangle_corners(
                            (0, 0), (t.get_value(), k / t.get_value())
                        )
                    ]
                )
                polygon.stroke_width = 1
                polygon.set_fill(m.BLUE, opacity=0.5)
                polygon.set_stroke(m.YELLOW_B)
                return polygon
    
            polygon = m.always_redraw(get_rectangle)
    
            dot = m.Dot()
            dot.add_updater(lambda x: x.move_to(ax.c2p(t.get_value(), k / t.get_value())))
            dot.set_z_index(10)
    
            self.add(ax, graph, dot)
            self.play(m.Create(polygon))
            self.play(t.animate.set_value(10))
            self.play(t.animate.set_value(k / 10))
            self.play(t.animate.set_value(5))
    
    
    if __name__ == '__main__':
        import os
        from pathlib import Path
    
        FLAGS = "-pqm"
        SCENE = "PolygonExample"
    
        file_path = Path(__file__).resolve()
        os.system(f"manim {Path(__file__).resolve()} {SCENE} {FLAGS}")
    

```


```{eval-rst}
.. manim:: AxesExample
    :save_last_frame:
    
    
    import manim as m
    import numpy as np
    
    from manim_themes.manim_theme import apply_theme
    
    
    class AxesExample(m.Scene):
    
        def setup(self):
            # Set the background color to a light beige
            theme = "Ubuntu"
            apply_theme(manim_scene=self, theme_name=theme)
            m.Text.set_default(font="Courier New", color=m.GREEN)
            m.Tex.set_default(color=m.RED)
            m.MathTex.set_default(color=m.RED)
    
        def construct(self):
            axes = m.Axes(
                x_range=[-10, 10.3, 1],
                y_range=[-1.5, 1.5, 1],
                x_length=10,
                axis_config={"color": m.GREEN},
                x_axis_config={
                    "numbers_to_include": np.arange(-10, 10.01, 2),
                    "numbers_with_elongated_ticks": np.arange(-10, 10.01, 2),
                },
                tips=False,
            )
            axes_labels = axes.get_axis_labels()
            sin_graph = axes.plot(lambda x: np.sin(x), color=m.BLUE)
            cos_graph = axes.plot(lambda x: np.cos(x), color=m.RED)
    
            sin_label = axes.get_graph_label(
                sin_graph, "\\sin(x)", x_val=-10, direction=m.UP / 2
            )
            cos_label = axes.get_graph_label(cos_graph, label="\\cos(x)")
    
            vert_line = axes.get_vertical_line(
                axes.i2gp(m.TAU, cos_graph), color=m.YELLOW, line_func=m.Line
            )
            line_label = axes.get_graph_label(
                cos_graph, r"x=2\pi", x_val=m.TAU, direction=m.UR, color=m.WHITE
            )
    
            plot = m.VGroup(axes, sin_graph, cos_graph, vert_line)
            labels = m.VGroup(axes_labels, sin_label, cos_label, line_label)
            self.add(plot, labels)
    
    
    if __name__ == '__main__':
        import os
        from pathlib import Path
    
        FLAGS = "-pqm"
        SCENE = "AxesExample"
    
        file_path = Path(__file__).resolve()
        os.system(f"manim {Path(__file__).resolve()} {SCENE} {FLAGS}")
    

```



```{eval-rst}
.. manim:: TableExample
    :save_last_frame:
    
    
    import manim as m
    import numpy as np
    
    from manim_themes.manim_theme import apply_theme
    
    class TableExample(m.Scene):
    
        def setup(self):
            # Set the background color to a light beige
            #theme = "Retro"
            theme="Obsidian"
            apply_theme(manim_scene=self, theme_name=theme)
    
            m.Text.set_default(
                font="Courier New",
                color=m.WHITE
            )
            m.Tex.set_default(color=m.WHITE)
            m.MathTex.set_default(color=m.WHITE)
    
            # Mobjects
            m.Mobject.set_default(color=m.WHITE)
            m.VMobject.set_default(color=m.WHITE)
    
            m.Rectangle.set_default(color=m.RED)
            m.AnnotationDot.set_default(stroke_color=m.WHITE, fill_color=m.BLUE)
            m.Arc.set_default(stroke_color=m.WHITE)
            m.AnnularSector.set_default(color=m.WHITE)
    
    
            m.NumberPlane().set_default(
                background_line_style={
                    "stroke_color": m.RED,
                },
                x_axis_config={"stroke_color": m.GREEN},
                y_axis_config={"stroke_color": m.BLUE},
            )
            m.Arrow.set_default(color=m.GOLD)
            m.Dot.set_default(color=m.PURPLE)
    
    
        def construct(self):
            t0 = m.Table(
                [["First", "Second"],
                 ["Third", "Fourth"]],
                row_labels=[m.Text("R1"), m.Text("R2")],
                col_labels=[m.Text("C1"), m.Text("C2")],
                top_left_entry=m.Text("TOP"))
            t0.add_highlighted_cell((2, 2), color=m.GREEN)
            x_vals = np.linspace(-2, 2, 5)
            y_vals = np.exp(x_vals)
            t1 = m.DecimalTable(
                [x_vals, y_vals],
                row_labels=[m.MathTex("x"), m.MathTex("f(x)")],
                include_outer_lines=True)
            t1.add(t1.get_cell((2, 2), color=m.RED))
            t2 = m.MathTable(
                [["+", 0, 5, 10],
                 [0, 0, 5, 10],
                 [2, 2, 7, 12],
                 [4, 4, 9, 14]],
                include_outer_lines=True)
            t2.get_horizontal_lines()[:3].set_color(m.BLUE)
            t2.get_vertical_lines()[:3].set_color(m.BLUE)
            t2.get_horizontal_lines()[:3].set_z_index(1)
            cross = m.VGroup(
                m.Line(m.UP + m.LEFT, m.DOWN + m.RIGHT),
                m.Line(m.UP + m.RIGHT, m.DOWN + m.LEFT))
            a = m.Circle().set_color(m.RED).scale(0.5)
            b = cross.set_color(m.BLUE).scale(0.5)
            t3 = m.MobjectTable(
                [[a.copy(), b.copy(), a.copy()],
                 [b.copy(), a.copy(), a.copy()],
                 [a.copy(), b.copy(), b.copy()]])
            t3.add(m.Line(
                t3.get_corner(m.DL), t3.get_corner(m.UR)
            ).set_color(m.RED))
            vals = np.arange(1, 21).reshape(5, 4)
            t4 = m.IntegerTable(
                vals,
                include_outer_lines=True
            )
            g1 = m.Group(t0, t1).scale(0.5).arrange(buff=1).to_edge(m.UP, buff=1)
            g2 = m.Group(t2, t3, t4).scale(0.5).arrange(buff=1).to_edge(m.DOWN, buff=1)
            self.add(g1, g2)
    
    
    if __name__ == '__main__':
        import os
        from pathlib import Path
    
        FLAGS = "-pqm -s"
        SCENE = "TableExample"
    
        file_path = Path(__file__).resolve()
        os.system(f"manim {Path(__file__).resolve()} {SCENE} {FLAGS}")
    

```


```{eval-rst}
.. manim:: ThemeCarouselObjects
    
    
    import manim as m
    import random
    
    from manim_themes.manim_theme import apply_theme
    from manim_themes.theme_preview import theme_preview
    
    
    class ThemeCarouselObjects(m.Scene):
    
    
        def construct(self):
            themes = ['Isocon Light',
                      'Pyrokai',
                      'Canyon Shadow',
                      'Solarized Osaka Night',
                      'X Helsinki',
                      'X',
                      'Subliminal',
                      'datum (dark)',
                      'Coffee Theme',
                      'Noctis Lux',
                      'Calamity',
                      'Sonoran Dusk',
                      'Adobe Moon',
                      'Cobalt Next',
                      'Jellybeans',
                      'The Hulk',
                      'Everforest Light Hard',
                      'Karasu Night',
                      'Grape',
                      'Iceberg Dark',
                      'Red Alert',
                      'SeedFlip Nightfall',
                      'Cool Night',
                      'Modus Vivendi Tritanopia',
                      'Liquid Carbon',
                      'iTerm2 Smoooooth',
                      'Obsurdian',
                      'Opaline',
                      'Apple System Colors',
                      'Clockwork Gold',
                      'Petrified',
                      'Catppuccin Frappe',
                      'Tinacious Design Light',
                      'Golden Retriever Cream',
                      'Chalkboard',
                      'No Clown Fiesta Light',
                      'Hopscotch',
                      'Later This Evening',
                      'GitHub Light Colorblind',
                      'Kibble',
                      'Rhoads RR Black',
                      'SeedFlip Carbon',
                      'Prickly Pear',
                      'SeedFlip Pulse',
                      'CRT Amber',
                      'Terminal Basic Dark',
                      'X Lahabana',
                      'Poimandres Darker',
                      'Tailwind Dark',
                      'Banana Blueberry',
                      'Abernathy',
                      'Karma Light Dimmed',
                      'X Madrid',
                      'Catppuccin Macchiato',
                      'Arthur',
                      'No Clown Fiesta',
                      'Jackie Brown',
                      'Galizur',
                      'Andromeda',
                      'Sonokai',
                      'Ollie',
                      'Carbon Paper',
                      'Sunset Drive',
                      'iTerm2 Pastel Dark Background',
                      'Firefly Traditional',
                      'Firefox Dev',
                      'Pencil Light',
                      'Kanagawa Wave',
                      'Atom One Dark',
                      'Aztec Sunset',
                      'IC Orange PPL',
                      'Pandora',
                      'Hipster Green',
                      'Phala Green Dark',
                      'Violet Light',
                      'Copper Canyon',
                      'Kanso Pearl',
                      'Claude Dark',
                      'Porcelain',
                      'C64',
                      'Mariana',
                      'Desert Moon',
                      'Builtin Tango Dark',
                      'Mellifluous',
                      'Gruber Darker',
                      'Y2K Chrome',
                      'Aura Dark',
                      'Aardvark Ink',
                      'TokyoNight Moon',
                      'Ghost Circuit',
                      'Royal',
                      'Everforest Dark Soft',
                      'Framer',
                      'SeedFlip Ember',
                      'Electron Highlighter Day',
                      'Heeler',
                      'Spacegray',
                      'Karma Dark',
                      'ENCOM',
                      'Sea Shells',
                      'Horizons',
                      'Numbers Station',
                      'Xcode Dark',
                      'Klein Void',
                      'EVH FrankenTone',
                      'Outrun Electric',
                      'IRIX Console',
                      'Clear Dark',
                      'Atom',
                      'Twilight',
                      'Safety Glass',
                      'Sandstone Classic',
                      'Symfonic',
                      'Syncopation',
                      'Material Ocean',
                      'Vimbones',
                      'Neobones Light',
                      'Tomorrow',
                      'Glacier',
                      'Serendipity Morning',
                      'Patina Light',
                      'SeedFlip Ivory',
                      'Flatland',
                      'Highway',
                      'Urple',
                      'Spiderman',
                      'Nightfall',
                      'Material Darker',
                      'Catppuccin Latte',
                      'Matcha Zen',
                      'urban',
                      'X Tokio',
                      'Birds Of Paradise',
                      'Thermal Receipt',
                      'cyberpunk-icy',
                      'London Columbia Road',
                      'Daybreak',
                      'Velvet Court',
                      'Grass',
                      'Gruvbox Material Light',
                      'Selenized Light',
                      'Retro',
                      'iTerm2 Tango Dark',
                      'SeedFlip Inkwell',
                      'Spacegray Eighties',
                      'Hopscotch.256',
                      'Espresso Libre',
                      'Flat',
                      'Blueprint',
                      'Karasu Snow',
                      'Neopolitan',
                      'Warm Burnout Dark',
                      'Dogxi Misty',
                      'Wryan',
                      'Dark 2026',
                      'Monokai Pro Light',
                      '3024 Day',
                      'Chalk',
                      'Pro',
                      'Poimandres',
                      'Sun Bleached',
                      'CGA',
                      'Sequoia Retro Dark',
                      'Zenwritten Dark',
                      'Monokai Pro Octagon',
                      'IC Green PPL',
                      'X Paris',
                      'Springfield Resident Hight Contrast',
                      'Dracula+ High Contrast',
                      'Golden Retriever Honey',
                      'Violet Dark',
                      'Zenburned',
                      'SeedFlip Coral',
                      'One Half Light',
                      'Sundried',
                      'Afterimage',
                      'HaX0R Blue',
                      'Dark+',
                      'Rippedcasts',
                      'Zenwritten Light',
                      'Seoulbones Light',
                      'Dot Gov',
                      'Cursor Dark',
                      'base16-icy',
                      'Black Metal (Nile)',
                      'Noctis Bordo',
                      'Sleepy Hollow',
                      'SeedFlip Glacier',
                      'Melange Dark',
                      'Warm Burnout Light',
                      'Kanagawabones',
                      'novmbr',
                      'One Half Dark',
                      'Medallion',
                      'Material',
                      'Black Metal (Marduk)',
                      'Monokai Vivid',
                      'Flexoki Light',
                      'Vercel',
                      'Onenord Light',
                      'Adwaita',
                      'TokyoNight Day',
                      'Cyberpunk',
                      'Black Metal (Burzum)',
                      'X Praha',
                      'Japanesque',
                      'TokyoNight Night',
                      'Dimidium',
                      'GitHub Dark',
                      'Earl Grey',
                      'Willow Grove',
                      'Cassette Tape',
                      'Alabaster',
                      'GitLab Light',
                      'Raycast Dark',
                      'Blazer',
                      'Belafonte Night',
                      'Modus Operandi Deuteranopia',
                      'Fairyfloss',
                      'Northstar',
                      'IRIX Terminal',
                      'Kanso Mist',
                      'JetBrains Islands Dark',
                      'Django',
                      'Golden Retriever Red',
                      'Terafox',
                      'Ayu',
                      'Black Metal (Immortal)',
                      'Selenized Dark',
                      'Toy Chest',
                      'Purple Rain',
                      'Dead Letter Office',
                      'Warm Neon',
                      'Static Memory',
                      'Pro Light',
                      'GitHub Dark High Contrast',
                      'Idle Toes',
                      'Monokai Classic',
                      'Seoulbones Dark',
                      'Kwyjibo',
                      'SeedFlip Amethyst',
                      'Monokai Pro Ristretto',
                      'Gruvbox Light',
                      'Mathias',
                      'Broadcast',
                      'Farmhouse Dark',
                      'GitHub Light High Contrast',
                      'SilkCircuit Glow',
                      'Lavandula',
                      'Solarized Dark Higher Contrast',
                      'Rhoads Insipired',
                      'Scarlet Protocol',
                      '0x96f',
                      'Zenbones',
                      'Nocturnal Winter',
                      'Green Screen',
                      'owl',
                      'Farmhouse Light',
                      'Kurokula',
                      'Flexoki Dark',
                      'Seti',
                      'Mesa Blue',
                      'Xcode Dark hc',
                      'Elemental',
                      'Noctis Minimus',
                      'Rose Pine Dawn',
                      'Chester',
                      'Kanagawa Lotus',
                      'Mona Lisa',
                      'Clear Light',
                      'Night Owl',
                      'JetCalm Light',
                      'Slate',
                      'Poimandres White',
                      'Deep Current',
                      'Synthwave Alpha',
                      'Driftwood',
                      'Monospace Dark',
                      'Night Owlish Light',
                      'Tailwind Light',
                      'Charcoal',
                      'Ultra Dark',
                      'Daybreaker',
                      'Trapped in Amber',
                      'Night Lion V1',
                      'Builtin Dark',
                      'Duskfox',
                      'Builtin Tango Light',
                      'Monokai SublimeText',
                      'Everforest Light Med',
                      'Darkside',
                      'Selenized Black',
                      'Catthode',
                      'X Bogota',
                      'Spring',
                      'Desert Bloom',
                      'Aizen Light',
                      'Amber CRT Retro',
                      'Vaughn',
                      'Xcode Light',
                      'Emberglass',
                      'Apple System Colors Light',
                      'Nord',
                      'Blue Matrix',
                      'Dawnfox',
                      'SeedFlip Phosphor',
                      'Tomorrow Night Bright',
                      'Ryuuko',
                      'Sumi Phosphor',
                      'Hybrid',
                      'Redacted',
                      'Monokai Soda',
                      'Blue Berry Pie',
                      'Ocotillo',
                      'Wild Cherry',
                      'Patina Lichen',
                      'Miami Heat',
                      'Raycast Light',
                      'Shokunin',
                      'Modus Operandi',
                      'Miasma',
                      'Solarized Dark Patched',
                      'Doom One',
                      'Modus Operandi Tinted',
                      'Modus Vivendi Deuteranopia',
                      'Sequoia Monochrome Dark',
                      'Neon',
                      'Konsolas',
                      'X London',
                      'Monokai Pro Spectrum',
                      'Guezwhoz',
                      'Catppuccin Mocha',
                      'Rhoads Concord',
                      'One Double Light',
                      'Kanso Zen',
                      'Kitty Low Contrast',
                      'Bluloco Light',
                      'Atelier Sulphurpool',
                      'Oceanic Material',
                      'Laser',
                      'Light 2026',
                      'Aurora Drift',
                      'Adwaita Dark',
                      'Terminal Green 1999',
                      'Havn Skumring',
                      'Ardoise',
                      'Patina Moss',
                      'Rose Pine',
                      'Kitty Default',
                      'Starlight',
                      'Modus Vivendi Tinted',
                      'Kanso Ink',
                      'Ayu Mirage',
                      'Cobalt Next Minimal',
                      'X Miami',
                      'Cholla',
                      'Tearout',
                      'Crayon Pony Fish',
                      'Tango Adapted',
                      'Thayer Bright',
                      'Emerald Synth',
                      'Black Metal',
                      'Molten Core',
                      'Elegant',
                      'Sandstone Ink',
                      'Atom One Light',
                      'Sandstone Warm',
                      'Rouge 2',
                      'Grok Night',
                      'Desert',
                      'Red Rock',
                      'Blue Dolphin',
                      'Spacegray Bright',
                      '12-bit Rainbow',
                      'SilkCircuit Dawn',
                      'Paper Tiger',
                      'SilkCircuit Neon',
                      'Night Pharmacy',
                      'Apple Classic',
                      'After Hours',
                      'GitLab Dark Grey',
                      'SeedFlip Ultraviolet',
                      'Afterglow',
                      'Purple Portal',
                      'Cactus Bloom',
                      'SeedFlip Wavelength',
                      'Pierre Dark',
                      'Nvim Dark',
                      'Gruvbox Dark Hard',
                      'Misterioso',
                      'Last Broadcast',
                      'Hot Dog Stand (Mustard)',
                      'Vacuum Tube',
                      'Synthwave',
                      'Isocon Dark',
                      'Adventure',
                      'RadicalReborn',
                      'Novel',
                      'Xcode WWDC',
                      'Lemon Graphite',
                      'Embark',
                      'Violite',
                      'Challenger Deep',
                      'iTerm2 Default',
                      'London Embankment Dusk',
                      'Signal Ghost',
                      'Niji',
                      'Neon Analog',
                      "Madman's Diary",
                      'Claude Light',
                      'Monospace Light',
                      'GitHub Light Default',
                      'Piatto Light',
                      'Gruvbox Light Hard',
                      'Under The Sea',
                      'Ubuntu',
                      'Prince of Darkness',
                      'Modus Vivendi',
                      'Kolorit',
                      'Verdigris',
                      'Sequoia Moonlight Dark',
                      'Sauber',
                      'Karma Light HC',
                      'Aura',
                      'Cobalt2',
                      'Iceberg Light',
                      'Smyck',
                      'Squintless',
                      'Tomorrow Night Eighties',
                      'Mesila One',
                      'Zenbones Light',
                      'Builtin Pastel Dark',
                      'HaX0R R3D',
                      'Vesper',
                      'Agave Dusk',
                      'Patina Stellar',
                      'Ember Peak',
                      'Teerb',
                      'Gruvbox Dark',
                      'Forest Blue',
                      'Oxocarbon',
                      'Nebula Drift',
                      'Breeze',
                      'Purplepeter',
                      'Whimsy',
                      'Monokai Pro Machine',
                      'Deep',
                      'Bright Lights',
                      'Nvim Light',
                      'Spacegray Eighties Dull',
                      'Darkmatrix',
                      'GitLab Dark',
                      'Nordfox',
                      'Zenburn',
                      'Dark Modern',
                      'Idea',
                      'Cyberpunk Scarlet Protocol',
                      'Eventide',
                      'Saguaro',
                      'Dalton Dark',
                      'Material Dark',
                      'Molokai',
                      'Pale Night Hc',
                      'Fun Forrest',
                      'Darkermatrix',
                      'Dimmed Monokai',
                      'Black Box Recorder',
                      'Adventure Time',
                      'Sugarplum',
                      'Hyper',
                      'Pierre Light',
                      'Elementary',
                      'HaX0R Gr33N',
                      'Gleam Classic',
                      'Noctis Lilac',
                      'Claude',
                      'Galaxy',
                      'N0Tch2K',
                      'Pencil Dark',
                      'Nord Wave',
                      'Aubade',
                      'Hardcore',
                      'Pnevma',
                      'Monokai Pro',
                      'Black Metal (Dark Funeral)',
                      'Aurora',
                      'Serendipity Sunset',
                      'Duotone Dark',
                      'Floraverse',
                      'Patina',
                      'Dayfox',
                      'Kanagawa Dragon',
                      'GitHub Dark Dimmed',
                      'Xcode Light hc',
                      'Operator Mono Dark',
                      'Earthsong',
                      'Melange Light',
                      'SeedFlip Voltage',
                      'Parchment',
                      'Sedona',
                      'Tomorrow Night Burns',
                      'Patina Dark',
                      'Gruvbox Material',
                      'iTerm2 Tango Light',
                      'Jubi',
                      'iTerm2 Light Background',
                      'X Oslo',
                      'Neon Purple',
                      'Modus Operandi Tritanopia',
                      'Firewatch',
                      'Green Phosphor CRT',
                      'JetBrains Darcula',
                      'Forge Ember',
                      'Monokai Remastered',
                      'Nightfox',
                      'Acid Lime',
                      'Material Design Colors',
                      'Black Metal (Khold)',
                      'Motel Vacancy',
                      'Relaxed',
                      'Primary',
                      'Gruvbox Material Dark',
                      'Midnight Arcade',
                      'GitHub Dark Colorblind',
                      'Zenbones Dark',
                      'Serendipity Midnight',
                      'Token Dark',
                      'Barrel Cactus',
                      'Powershell',
                      'Light Owl',
                      "Ozz's Blizzard",
                      'Snazzy Soft',
                      'Wombat',
                      'Cutie Pro',
                      'Tomorrow Night Blue',
                      'Embers Dark',
                      'Keys Ocean Sunset',
                      'Monokai Pro Light Sun',
                      'Horizon',
                      'Liquid Carbon Transparent',
                      'Shaman',
                      'Fish Tank',
                      'CLRS',
                      'Seafoam Pastel',
                      'Cursor Light',
                      'Doom Peacock',
                      'Brogrammer',
                      'Arcoiris',
                      'Hacktober',
                      'Front End Delight',
                      'Vaporwave Sunset',
                      'Aizen Dark',
                      'Poimandres Storm',
                      'Squirrelsong Dark',
                      'Night Lion V2',
                      'Dracula+',
                      'Rapture',
                      'Icy Glacier',
                      'Black Metal (Bathory)',
                      'SilkCircuit Soft',
                      'Sakura',
                      'Dark Pastel',
                      'Hivacruz',
                      'Gleam',
                      'Cobalt Neon',
                      'Rebecca',
                      'Dracula',
                      'IBM 5153 CGA',
                      'Obsidian',
                      'Noctis',
                      'High Desert Snow',
                      'Sumi Linen',
                      'Black Metal (Venom)',
                      'Matrix',
                      'Srcery',
                      'GitHub',
                      'Desert Thunder',
                      'Everforest Light Soft',
                      'Django Reborn Again',
                      'Solar Flare',
                      'Vague',
                      'Atlas Ragnarok',
                      'Ember',
                      'Wez',
                      'Red Sands',
                      'Shades Of Purple',
                      'Karma Dark Dimmed',
                      'Mirage',
                      'Midnight In Mojave',
                      'Mesa Twilight',
                      'Nord Light',
                      'Karma Light',
                      'Red Planet',
                      'Synthwave Everything',
                      'Man Page',
                      'Wilmersdorf',
                      'Moonwalk',
                      'London Bonfire Night',
                      'Turquoise Trail',
                      'Keys Ocean Sunset HC',
                      'Havn Daggry',
                      'Breadog',
                      'Alien Blood',
                      'Painted Desert',
                      'Unikitty',
                      'SeedFlip Canopy',
                      'Rhoads Legacy',
                      'Oxide',
                      'TokyoNight',
                      'Batman',
                      'Lunar Dust',
                      'Arizona Monsoon',
                      'Tango Half Adapted',
                      'Springfield Resident',
                      '3024 Night',
                      'Retro Legends',
                      'Lab Fox',
                      'One Dark Two',
                      'Noctis Sereno',
                      'Terminal Basic',
                      'Harper',
                      'Homebrew',
                      'Grey Green',
                      'Tinacious Design Dark',
                      'traffic',
                      'Argonaut',
                      'Fahrenheit',
                      'Solarized Darcula',
                      'Cyberdyne',
                      'Bluloco Dark',
                      'Eclipse',
                      'Black Metal (Gorgoroth)',
                      'Pueblo Night',
                      'iTerm2 Solarized Dark',
                      'Aardvark Blue',
                      'Ayu Light',
                      'White Sands',
                      'Graphite',
                      'Espresso',
                      'Noctis Hibernus',
                      'Oceanic Next',
                      'Grok Day',
                      'Overnight Slumber',
                      'X Berlin',
                      'iTerm2 Dark Background',
                      'Patina Dark Soft',
                      'Prism',
                      'Paraiso Dark',
                      'Sequoia Moonlight Light',
                      'Everforest Dark Med',
                      'Spacedust',
                      'Caliche',
                      'Cold Storage',
                      'Rose Pine Moon',
                      'Snazzy',
                      'Citrus Ink',
                      'Token Light',
                      'Sequoia Monochrome Light',
                      'Matte Black',
                      'Frostline',
                      'Electron Highlighter',
                      'Borland',
                      'Django Smooth',
                      'Onenord',
                      'Oxblood',
                      'Letterpress',
                      'Builtin Light',
                      'Popping And Locking',
                      'Paul Millr',
                      'Noctis Azureus',
                      'Desert Rose',
                      'Everforest Dark Hard',
                      'Noctis Obscuro',
                      'Ciapre',
                      'Sequoia Retro Light',
                      'Citruszest',
                      'Neutron',
                      'Noctis Viola',
                      'Hurtado',
                      'Duckbones',
                      'Treehouse',
                      'Moonfly',
                      'One Double Dark',
                      'GitHub Dark Default',
                      'Sublette',
                      'branch',
                      'Horizon Bright',
                      'datum (light)',
                      'CRT Afterglow',
                      'IR Black',
                      'Frostbyte',
                      'Box',
                      'Ghostty Default Style Dark',
                      'SilkCircuit Vibrant',
                      'Peppermint',
                      'Mellow',
                      'Tomorrow Night',
                      'Noctis Uva',
                      'Fideloper',
                      'Evergreen',
                      'Soft Server',
                      'Neobones Dark',
                      'Carbonfox',
                      'Ultra Violent',
                      'Monsoon Mesa',
                      'Everblush',
                      'Vibrant Ink',
                      'Ocean',
                      'SeedFlip Abyss',
                      'Lovelace',
                      'Cobalt Next Dark',
                      'Nachtschicht',
                      'Black Metal (Mayhem)',
                      'Karma Dark HC',
                      'TokyoNight Storm',
                      'Belafonte Day',
                      'Hot Dog Stand',
                      'iTerm2 Solarized Light',
                      'London Soho Night',
                      'Pyrokai Light',
                      'Rhoads LP',
                      'IBM 5153 CGA (Black)',
                      'Square',
                      'Detuned']
            random.shuffle(themes)
            # get a random sample of 20 themes from the list
            # every time the docs are built, a different set of themes is shown :)
            for theme in themes[:20]:
                apply_theme(manim_scene=self, theme_name=theme, light_theme=True)
    
                ax = m.Axes(
                    x_range=[0, 5],
                    y_range=[0, 6],
                    x_axis_config={"numbers_to_include": [2, 3]},
                    tips=False,
                )
    
                labels = ax.get_axis_labels()
    
                curve_1 = ax.plot(lambda x: 4 * x - x ** 2, x_range=[0, 4], color=m.BLUE_C)
                curve_2 = ax.plot(
                    lambda x: 0.8 * x ** 2 - 3 * x + 4,
                    x_range=[0, 4],
                    color=m.GREEN_B,
                )
    
                line_1 = ax.get_vertical_line(ax.input_to_graph_point(2, curve_1), color=m.YELLOW)
                line_2 = ax.get_vertical_line(ax.i2gp(3, curve_1), color=m.YELLOW)
    
                riemann_area = ax.get_riemann_rectangles(curve_1, x_range=[0.3, 0.6], dx=0.03, color=m.BLUE, fill_opacity=0.5)
                area = ax.get_area(curve_2, [2, 3], bounded_graph=curve_1, color=m.GREY, opacity=0.5)
    
                graph_group = m.VGroup(ax, labels, curve_1, curve_2, line_1, line_2, riemann_area, area)
                graph_group.scale(0.5)
                graph_group.to_edge(m.LEFT)
    
                theme_label = m.Text(
                    text=theme,
                    font="Courier New",
                )
                theme_label.to_edge(m.UP, buff=0.5)
    
                m0 = m.Dot()
                m1 = m.AnnotationDot()
                m2 = m.LabeledDot("ii")
                m3 = m.LabeledDot(m.MathTex(r"\alpha").set_color(m.ORANGE))
                m4 = m.CurvedArrow(2 * m.LEFT, 2 * m.RIGHT, radius=-5)
                m5 = m.CurvedArrow(2 * m.LEFT, 2 * m.RIGHT, radius=8)
                m6 = m.CurvedDoubleArrow(m.ORIGIN, 2 * m.RIGHT)
    
                m_group = m.VGroup(m0, m1, m2, m3, m4, m5, m6).arrange(m.DOWN, buff=0.2)
    
                m_group.next_to(graph_group, m.RIGHT)
    
                circle = m.Circle()
                square = m.Square()
    
                geo_group = m.VGroup(circle, square).arrange(m.DOWN, buff=0.2)
                geo_group.next_to(m_group, m.RIGHT)
    
                self.add(graph_group, theme_label, m_group, geo_group)
    
                self.wait(0.5)
    
                self.remove(graph_group, theme_label, m_group, geo_group)
    
    if __name__ == '__main__':
        import os
        from pathlib import Path
    
        FLAGS = "-pqm"
        SCENE = "ThemeCarouselObjects"
    
        file_path = Path(__file__).resolve()
        os.system(f"manim {Path(__file__).resolve()} {SCENE} {FLAGS}")
    

```

