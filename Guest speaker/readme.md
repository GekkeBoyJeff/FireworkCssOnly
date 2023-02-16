**Moving features from JS to CSS & HTML**
`By Kilian Valkhof`

## Wie is kilian
Zijn naam is Kilian Valkhof, hij heeft de afgelopen 20 jaar websites gebouwd.
Hij is onderdeel van het **electron governance team**.
Is een maker van de Polypane browser.

Hij houdt van HTML, CSS en JS vanwege het volgende:

- De wet van de meeste macht : **Choose the least powerfull language suitable for a given perpose**

Als je iets in HTML kan doen, doe het in html. 
Kan het in CSS, doe het dan in CSS.
Daarna kijk je pas naar Javscript.

**Browser makers are listening**
And are implementing the stuff we built by hand.

## Er zijn verschillende HTML en CSS dingen uitgevonden in de laatste jaren om dingen te bouwen zonder javascript

### Een label koppelen aan je input / checkbox
```HTML
<label>
    <input type="checbox"/>
    My awesome feature
</label>

<!-- of gebruik een for attribuut op de label. -->
```
![](./images/Pasted%20image%2020230216122256.png)

### Input elementen kan je stylen.
```CSS
input{
    appearance:none;
    position:relative;
    display:inline-block;
    background:lightgray;
    height:1.5rem;
    width:2.7rem;
    verticle-align:middle;
    border-radius:2rem;
    box-shadow: 0 1px 3px #000;
    transition: .25s ease;
```
Appearance:none; is de truq. Hiermee zeg je tegen je browser dat jij je styling regelt.

### Gebruik focus-visible
```CSS
input:focus-visible{
    /* voor als je gaat tabben. */
}
input::before{
    // je styling
}
input:checked::before{
    /** je styling als het gechecked is.  */
}
```

### Data list
```HTML
<input list="frameworks"/>
<datalist id="frameworks">
    <option>Bootstrap></option>
    <option>Bootstrap2></option>
    <option>Bootstrap3></option>
</datalist>
```
![](./images/Pasted%20image%2020230216122653.png)

### input elementen hebben een browser pre-configured dark mode dit kan je aanzetten met:
```CSS
input{
    color-scheme:dark;
}
```

### Pagina transities
Met scroll-behaviour: smooth; zorg je dat je browser mooi naar een element toe scrollt.

### Denk aan accessibility!
```CSS
@media( prefers-reduces-motion: no-preference ){
    html{
    scroll-behavior:smooth;
    }
}
```

### Scrollen naar ID met extra ruimte bovenin.
```CSS
#myTarget{
    Scroll-margin-top:100px;
    /* Scroll-padding-top:100px; */
}
```

### Extra aandacht naar gescrollde element.
```CSS
#myTarget:target{
    outline: 1em solid red;
    transition: 1s ease-in-out outline;
}
```

### Position sticky kan je gebruiken om elementen vast te zetten en responsive te houden.
```CSS
.sticky{
    position:sticky;
    top:2em;
}
```

### Carousels bouwen
Dit kan je doen met scroll snapping. Scroll-snap verteld de browser waar de scroll moet stoppen.
```CSS
.container{
    scroll-snap-type: x mandatory;
}
.item{
    scroll-snap-align: center;
}
```
![](./images/Pasted%20image%2020230216123137.png)
Scroll-snap-align is een **logical property**

Extra demo: youtu.be/34zcWFLCDlc
`Adam Argyle`

### Masonry layout
```CSS
.container{
    display:grid;
    grid-template-columns:repeat(4, 1fr);
    grid-template-rows: masonry;
}
```
![](./images/Pasted%20image%2020230216123236.png)

### Select menu
Je kan niets doen om de select te stijlen.

Daarintegen komt **selectmenu** binnenkort wel uit als preview. Het kan wel nog wat langer duren voordat het word geimplementeerd in de meeste browsers.
```HTML
<selectmenu></selectmenu>
```

Ieder onderdeel is stijlbaar:
```CSS
selectmenu::part(button){ }
selectmenu::part(listbox){ }
selectmenu option){ }
```

### Container queries
In plaats van een media query heb je een container query. Dan kijk je naar de breedte van het element in plaats van het scherm.
```CSS
@container(max-width:4em){

}
```

### The parent selector :has()
```CSS
form:has(#other:checked) #other-text{
    display:block;
}
```
https://polypane.app/where-is-has

### Scroll linked animation
Een keyframe koppelen aan je scroll positie van ieder scrollbaar element.
Het is te koppelen met scroll-snap-type. Echter is het nog niet uit.
![](./images/Pasted%20image%2020230216124011.png)

### Lazyloading
```HTML
<img src="" alt="" loading="Lazy">
```

### Download attribuut
```HTML
<a href="asd.pdf" download></a>
```

### Accordions en toggles
Met details en summary element heb je een native oplossing hiervoor.

```HTML
<details> <!-- of <details open> om het standaard open te hebben -->
    <summary>here is my title</summary>
    <p>Here is my paragraph</p>
</details
```

#### Het pijltje hiervoor kan je weghalen met het marker element.
```CSS
summary::marker{
    content:'';
}
[open] summary::marker{
    content:'>'
}
```

##### Vergeet geen indicatie toe te voegen om het klikbaar te maken.
```CSS
summary:hover{
    cursor:pointer;
}
```

### Dialog element (niet geheel zonder js)
Dialog zit in de top-layer van je pagina. Het lijkt enorm op de error popup van javascript maar deze werkt zonder javascript en blokkeert niet je hele pagina. Ook heeft de dialog altijd een top-level z-index en beschikt Dialog ook over een backdrop. Meer hierover lees je hieronder.
![](./images/Pasted%20image%2020230216124312.png)
```HTML
<dialog>
    <form method="dialog">
        <h1>Test</h1>
        <button type="submit">Close</submit>
    </form>
<dialog>
```
Dit kan je laten zien met javascript.
```HTML
<button onclick="$$('dialog).showModal()'"
```

Of als je mensen een keuze wilt geven:
```HTML
<dialog>
    <form method="dialog">
        <h1>Test</h1>
        <button type="submit" value="wrong">Close</submit>
        <button type="submit" value="right">Close</submit>
    </form>
<dialog>
```
Kijk hierboven naar de values die je meegeeft. Daarmee kan je via javascript weer dingen doen.

Dialog heeft een backdrop dat de op één na hoogste laag heeft. Hierdoor kan je het achtergrond donkerder maken of blurren.

**Polypane blog heeft een dialog blogpagina die dit uitlegt**

