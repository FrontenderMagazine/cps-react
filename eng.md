<section name="e8f2" class="section section--body section--first" score="41.25
"><figure name="ca73" id="ca73" class="graf graf--figure graf--layoutFillWidth
graf-after--h3" score="-12.5
">![][1]<figcaption class="imageCaption">Component Model ⤑ (+ Application
Logic ) ⤑ ((+ UI )) ⤑ ((( React Application
)))</figcaption></figure>

Let’s imagine that we design clean Component Model, like this:

    <**Application**>  
    <**Tree**/>  
    <**Grid**>  
    <**Combo**/>  
    <**button**>*Add*</button>  
    <**button**>*Delete*</button>  
    </Grid>  
    </Application>

After adding application logic, the render will look like:<figure name="5cc1"
id="5cc1" class="graf graf--figure graf--iframe graf-after--p" score="-13.75
"></figure>

Pretty simple, isn’t it?

But finally, after applying UI mockup, it will turn out to be the something
like this:<figure name="c178" id="c178" class="graf graf--figure graf--iframe
graf-after--p" score="-13.75
"></figure>

We need to extract application logic **bindings** from`render()` method of our
application/component to the separated entity — let it be*Property Sheet*.

First, start with basic **Application Layout**:<figure name="cac9" id="cac9"
class="graf graf--figure graf--iframe graf-after--p" score="-13.75
"></figure>

Then add **State Management** bindings by the Property Sheet:<figure name="b500
" id="b500" class="graf graf--figure graf--iframe graf-after--p" score="-13.75
"></figure>

Next, extend Application Layout by creating **Bootstrap Layout**:<figure name="
7ee1" id="7ee1" class="graf graf--figure graf--iframe graf-after--p graf--last" 
score="-13.75
"></figure> </section><section name="eac4" class="section section--body" score
="41.25
">

<figure name="867b" id="867b" class="graf graf--figure graf--layoutOutsetLeft
graf--leading" score="-12.5
">![][2]</figure>

Now, as you can see, we have separated application logic in Application Layout
, and all UI-related code in Bootstrap Layout. So, we can easily switch layouts:
theoretically we can make mobile**React Native** app, that will **reuse
application logic** code!

> **This is the variation of **[**Container Components**][3]** pattern**, where
> many small Presentation Components can be replaced by one–two Presentation 
> Layout(s
> ).
> In HTML/CSS people use markup for data and CSS for styling.   
> CPS concept is the opposite: we should use markup for styling,   
> and** **Cascading Sheets to transfer the data.
    **applyPropsSheet**( this || this.propsSheet, React =>   
    <Application>*<!-- ... -->*<Application/> )

*   `applyPropsSheet()` temporary substitute [jsx pragma][4] by setting custom
   `React.createElement` (that’s purpose of `React =>` callback)
*   build tree of arrays`[type, props, ...childs]`(args for jsx pragma):

    [**Application**, null,  
    [**Tree**],  
    [**Grid**, null,  
    [ **Combo **],  
    [**'button'**, null, '*Add*'],  
    [**'button'**, null, '*Delete*']  
    ]  
    ]

*   add properties from PropsSheet to that tree
*   call real`React.createElement` on each node of the tree,  
    and return root react element</section><section name="9e5a" class="section
section--body section--last" score="33.75
"></section>

 [1]: img/1*0rmxebmdScJLBwLmbfHi7A.png
 [2]: img/1*WpV8LMzV1dprDEfJwUJ2qA.jpeg
 [3]: https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0
 [4]: https://babeljs.io/docs/plugins/transform-react-jsx/