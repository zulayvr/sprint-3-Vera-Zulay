/*
sprint 3: matematicas discretas:
Estudiante: Vera Rodriguez Zulay
C.I: 18209300
*/

:- use_module(library(http/thread_httpd)).
:- use_module(library(http/http_dispatch)).
:- use_module(library(http/html_write)).
:- use_module(library(http/html_head)).

:- use_module(library(http/http_client)).

:- http_handler(css('bootstrap.css'), http_reply_file('bootstrap.css', []), []).
:- http_handler(css('main.css'), http_reply_file('main.css', []), []).

:- html_resource(jquery, [virtual(true),
	   requires('https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js')]).
:- html_resource(bootstrap_js, [virtual(true), ordered(true),
	    requires([jquery, 'https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/js/bootstrap.min.js'])]).


:- html_resource(js_script('bootstrap.js'), [requires(js_script('jquery.min.js'))]).

http:location(css, root(css), []).
http:location(js_script, root(js_script), []).


:- http_handler('/', landing_pad, []).


servidor(Puerto) :-
        http_server(http_dispatch, [port(Puerto)]).


landing_pad(Request) :-

	reply_html_page(
	   [title('ULAnix Mathematica')],
	    [\page_content(Request)]).


page_content(_Request) -->
	html(
	   [\html_requires(css('bootstrap.css')),
	    \html_requires(css('main.css')),
	    \html_requires(jquery),
	    \html_requires(bootstrap_js),

	    \head,
	    \enlaces,
	    \temas,
	    \conjuntos,
	    \otro


     ]).


% **********************************************************************

:- http_handler('/logica', logica_landing_pad, []).

logica_landing_pad(Request) :-
        member(method(post), Request), !,
	   reply_html_page(
	   [title('Lógica')],
	    [\logica_page_content(Request)]).


logica_page_content(_Request) -->
	html(
	    [\html_requires(css('bootstrap.css')),
	    \html_requires(css('main.css')),
	    \html_requires(jquery),
	    \html_requires(bootstrap_js),

	    \head,
	    \enlaces,
\conjuntos


	]).




head --> html(header([div(class='img-responsive container row col-xs-12 col-sm-12 col-md-12 col-lg-12',img([src='http://s14.postimg.org/dossnbh4h/ULAnix.jpg', class='img-responsive', style='float: left; margin: 0px 0px 0px 100px;']))])).

%
enlaces --> html(form(method='POST', [

		 \[
		'<nav id="menu-responsive" class="navbar navbar-default" role="navigation">
		<div class="navbar-header"><button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-ex1-collapse "><span class="sr-only">Cambiar Navegación</span><span class="icon-bar"></span><span class="icon-bar"></span><span class="icon-bar"></span></button></div>
		<div class="container"><div id="menu" class="collapse navbar-collapse navbar-ex1-collapse venacti-white">

		<div><ul class="nav navbar-nav"><li><a href="/"><img src="http://s2.postimg.org/65fmgunf9/home.png"> Inicio</a></li><li class="dropdown"><a href="#" class="dropdown-toggle" data-toggle="dropdown"><img src="http://s12.postimg.org/howtipoh5/temas.png"> Temas<b class="caret"></b></a><ul class="dropdown-menu"><li><input name="submit" type="submit" class="btn btn-md btn-success btn-block" value="Lógica" formaction="/logica" formmethod="POST"></li><li><input name="submit" type="submit" class="btn btn-md btn-success btn-block" value="Conjuntos y Funciones" formaction="/" formmethod="POST"></li><li><input name="submit" type="submit" class="btn btn-md btn-success btn-block" value="Estructuras Algebraicas" formaction="/" formmethod="POST"></li><li><input name="submit" type="submit" class="btn btn-md btn-success btn-block" value="Inducción Matemática" formaction="/" formmethod="POST"></li><li><input name="submit" type="submit" class="btn btn-md btn-success btn-block" value="Combinatoria" formaction="/" formmethod="POST"></li><li><input name="submit" type="submit" class="btn btn-md btn-success btn-block" value="Funciones Generatrices" formaction="/" formmethod="POST"></li><li><input name="submit" type="submit" class="btn btn-md btn-success btn-block" value="Recurrencias" formaction="/" formmethod="POST"></li><li><input name="submit" type="submit" class="btn btn-md btn-success btn-block" value="Introducción a la Complejidad Computacional" formaction="/" formmethod="POST"></li>    </ul> </li><li><a href="http://nux.ula.ve"><img src="http://s12.postimg.org/8qgegjfah/bookmark.png"> ULAnix</a></li><li><a href="http://www.serbi.ula.ve/"><img src="http://s24.postimg.org/mjwzo1fgh/white_folder.png"> SERBIULA</a></li> </ul></ul>
   </div></div></div>
</nav>']

				     ]) ).



conjuntos --> html(form([style='align: left; margin: 0px 0px 0px 100px;', method='POST'], [

		p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'],
		  h4(class='venacti',b(' CONJUNTOS:  1.- Una noción más básica que la del número es la de conjunto, pero es necesario discutirla y aclararla
porque es la base de toda la Matemática. Trate de explicar que es un conjunto')))),p(div([label(['es una coleccion bien definida de objetos']),input([type='text',class='form-control'])])),

			   p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'],
		  h4(class='venacti',b('2.- ara indicar un conjunto se escriben sus elementos entre {}, así el conjunto A de los números enteros entre
-3 y 4 ambos incluidos es:')))),p(div([label(['A={-3,-2,-1,0,1,2,3}']),input([type='text',class='form-control'])])),

			   p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'],
		  h4(class='venacti',b('3- Según lo anterior el conjunto queda definido cuando se indican todos sus elementos. ¿Puede siempre
definirse así? __no___ Indique dos conjuntos que no pueden definirse de esta manera.')))),p(div([label(['A={1,2},A={0,1,2,3}']),input([type='text',class='form-control'])])),

			   p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'],
		  h4(class='venacti',b('4.- Los componentes de un conjunto se llaman elementos y se dicen que pertenecen al conjunto. La relación
“pertenece a” se indica . Así si: A= {a, z, , *, , } entonces ___∈__ A. La ∈ ⊙ △ ❒ ❒ idea de pertenecer ,
como la de conjunto es una idea intuitiva básica. "No pertenece" se indica ∉ o ∈ __1__ ∉ A')))),p(div([label(['']),input([type='text',class='form-control'])])),

			   p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'],
		  h4(class='venacti',b('5.- La manera usual de definir un conjunto es dar una regla tal que para todo objeto pueda decirse si
pertenece o no al conjunto. Ejemplo:')))),p(div([label(['A={x|x>0']),input([type='text',class='form-control'])])),

			   p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'],
		  h4(class='venacti',b('6.- La forma anterior de definir se expresa así formalmente: Sea P(x) una función proposicional con sentido
(puede ser sólo V ó F) para todo objeto x. Queda definido entonces el conjunto A de todas las x que hacen
verdadera P(x). Así si P(x) es x > 10 esto define al conjunto de los números mayores que 10.
Se indica así: A = {x | x > 10} donde: = significa "es" { significa "el conjunto de todos los " | significa
"tales que".')))),p(div([label(['significa los numeros mayores que 10']),input([type='text',class='form-control'])]))

			  ])).







temas --> html(form([style='align: left; margin: 0px 0px 0px 100px;'], [
		section(( p(['BIENVENIDOS AL CURSO DE MATEMÁTICAS DISCRETAS 1.- Considere el siguiente diálogo:
- ¿Para qué sirve la lógica?.
- Para explicar para qué sirve la lógica.
¿Tiene sentido? ¿Tiene lógica?']))),
			p(div([label(['Ejemplo.Logica:tiene sentido,hay conocimiento valido']),input([type='text',class='form-control'])])),

			   p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),	p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'], h4(class='venacti',b('2.- Los lógicos suelen afirmar que existen ciertas palabras cuyo significado trasciende todo tema
particular y, por tanto, se les puede considerar "palabras lógicas". La palabra "y" y la palabra "o",
son dos ejemplos.
¿Se te ocurren otros ejemplos?¿Cuál es el significado de estas palabras?')))),

		section(p(h7([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11 degraded container-planes'], p(['las palabras que sirven en cualquier contexto',
		p(div([label(['Ejemplo:si, siempre,sol,no, siempre y cuando']),

	input([ type='tet', class='form-control'])]


		       ))  ])))), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),	p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'], h4(class='venacti',b('3.- Si "o" significa lo que dice esta tabla:
')))),

		section(p(h7([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11 degraded container-planes'], p(['semántica de la o',
		p(div([label([' ']),

	input([name='submit', type='hidden', class='btn btn-md btn-success btn-block', value='tabla',action='/' ,formmethod='POST'])]


		       ))  ])))),table([tr([td(['p']),html(\['</td>']),td(['q']),html(\['</td>']),td(['p o q']),html(\['</td></tr>']),tr([td(['verdad']),html(\['</td>']),td(['verdad']),html(\['</td>']),td(['verdad']),html(\['</td></tr>']),tr([td(['verdad']),html(\['</td>']),td(['falso']),html(\['</td>']),td(['verdad']),html(\['</td></tr>'])])])]),tr([td(['falso']),html(\['</td>']),td(['verdad']),html(\['</td>']),td(['falso']),html(\['</td></tr>']),tr([td(['falso']),html(\['</td>']),td(['falso']),html(\['</td>']),td(['falso']),html(\['</td></tr>'])])])]),	section(p(h7([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11 degraded container-planes'], p(['semántica de la y',p(div([label(['']),


	input([name='hidden', type='hidden', class='btn btn-md btn-success btn-block', value='tabla',action='/' ,formmethod='POST'])]


		       ))  ])))),table([tr([td(['p']),html(\['</td>']),td(['q']),html(\['</td>']),td(['p y q']),html(\['</td></tr>']),tr([td(['verdad']),html(\['</td>']),td(['verdad']),html(\['</td>']),td(['verdad']),html(\['</td></tr>']),tr([td(['verdad']),html(\['</td>']),td(['falso']),html(\['</td>']),td(['falso']),html(\['</td></tr>'])])])]),tr([td(['falso']),html(\['</td>']),td(['verdad']),html(\['</td>']),td(['falso']),html(\['</td></tr>']),tr([td(['falso']),html(\['</td>']),td(['falso']),html(\['</td>']),td(['falso']),html(\['</td></tr>'])])])]), p(['semántica de la y/o',p(div([label(['']),
	input([name='hidden', type='hidden', class='btn btn-md btn-success btn-block', value='¿Cuál es el significado de "y/o"?.',action='/' ,formmethod='POST'])]


		       ))  ]),table([tr([td(['p']),html(\['</td>']),td(['q']),html(\['</td>']),td(['p y/o q']),html(\['</td></tr>']),tr([td(['verdad']),html(\['</td>']),td(['verdad']),html(\['</td>']),td(['verdad']),html(\['</td></tr>']),tr([td(['verdad']),html(\['</td>']),td(['falso']),html(\['</td>']),td(['verdad']),html(\['</td></tr>'])])])]),tr([td(['falso']),html(\['</td>']),td(['verdad']),html(\['</td>']),td(['verdad']),html(\['</td></tr>']),tr([td(['falso']),html(\['</td>']),td(['falso']),html(\['</td>']),td(['falso']),html(\['</td></tr>'])])])]),p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),	p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'], h4(class='venacti',b('4.- Una proposición es una oración que se puede asociar con un valor de verdad. Es decir, puede ser
verdadera o falsa. El lenguaje de la lógica proposicional, o lógica de enunciados, se construye sobre
proposiciones. Algunas veces las proposiciones son representadas por letras como p, q, r, s, w.')))),

		section(p(h7([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11 degraded container-planes'], p(['Para decir que p ',
		p(div([label(['es']),

	input([ type='tet', class='form-control'])]))])))),section(p(h7([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11 degraded container-planes'], p(['decimos que p = V. Dualmente, p es falsa si p  ',
		p(div([label(['=']),

	input([ type='tet', class='form-control'])]))])))), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),	p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'], h4(class='venacti',b('5.- Ocúpese de asignar valores a las proposiciones siguientes (a este, los lógicos lo llaman un
ejercicio de interpretación en lógica proposicional):')))),

		section(p(h7([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11 degraded container-planes'],p(['q = un triángulo tiene 4 lados',
		p(div([label(['q=F']),	input([ type='tet', class='form-control'])]))])))),	section(p(h7([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11 degraded container-planes'], p(['p = 3 es menor que 5, ',
		p(div([label(['p=V']),

	input([ type='tet', class='form-control'])]))])))), p([style='font-size: 15pt', title='Respuesta correcta'],'r = Ecuador está en America, r = V'),p([style='font-size: 15pt', title='Respuesta incorrecta'],             'r=F'),
	    p([style='font-size: 18pt', title='Respuesta correcta'], 's = Existe un círculo perfecto, s = V'),p([style='font-size: 18pt', title='Respuesta incorrecta'], 's = Existe un círculo perfecto, s = F'),
	    p([style='font-size: 15pt', title='Respuesta'], 'w = El rey de Venezuela es ateo, w = F_______ '),
	    p([style='font-size: 18pt', title='Pregunta'], 't = Los rectángulos son obligatorios,t = _______'), p([style='font-size: 18pt', title=''], 'u = la oración u es una mentira, u = _______'), p([style='font-size: 18pt', title='Pregunta'], 'z = la oración z es improbable, z = _______'), p([style='font-size: 18pt', title=''], '(NOTA: "u" y "z" son casos (muy) difíciles).
Ahora discuta los casos difíciles y sugiera como podrían evitarse esas dificultades.'), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),	p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'],
		  h3(class='venacti',b('6.- Las proposiciones anteriores son llamadas proposiciones simples. Las proposiciones simples se
suelen mostrar como una oración con sujeto y predicado, pero no tienen que ser así necesariamente
(piense en un ejemplo). Decidir sobre la verdad o falsedad de una proposición puede conducir a
problemas científicos o filosóficos no resueltos.
En lo que sigue trataremos un problema más simple: a: Supondremos que siempre se puede asignar
a una proposición bien el valor v (verdadera) o bien el valor f (falso). De esta forma, se comporta
como una variable que puede adoptar uno de dos valores; y b) Consideraremos proposiones compuestas formadas por dos o más proposiciones simples y discutiremos que valor de verdad debemos asignarles cuando se conocen los valores de verdad de la simpes.'))
		 )),	p(div([class='form-group col-xs-11 col-sm-11 col-md-11 col-lg-11',style='margin:0px;'],
		  h3(class='venacti',b('7.- Vamos a considerar el caso simple de una proposición compuesta formada por dos
proposiciones simples unidas por un "y". Juzgue el valor que daría a cada una y al conjunto en los
siguientes ejemplos, suponiendo las definiciones en los problemas previos.'))
		 )), p([style='font-size: 15pt', title='Respuesta correcta'],'w = Ecuador es un país y Ecuador está en América, es decir: p y q: V'), p([style='font-size: 15pt', title='Respuesta incorrecta'],' p y q: F'),
	    p([style='font-size: 18pt', title='Respuesta correcta'], 'u = El caracol es un animal y es un vertebrado = s y t: F'), p([style='font-size: 15pt', title='Respuesta incorrecta'],' s y t: V'),
	    p([style='font-size: 15pt', title='Respuesta'], 'Un banco le dará crédito al Sr. Fulano si es verdadero que:
r = el Sr. Fulano es solvente y el Sr Fulano tiene los documentos en regla = a y b.
¿En qué casos le daría crédito? (para valores de a y de b)._V_V_= V '), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))), p([style='font-size: 15pt', title='Pregunta'], '8.- Considere las tablas en el problema 3. La tabla inferior puede considerarse como la definición de
la operación "y" (algunas veces se escribe / , el techito, ó & ó ^ ) a partir de los valores de p y q (de
la misma manera que la tabla pitagórica define la multiplicación).
Note que nuestra variables p y q sólo pueden tomar los valores ___ o ____, mientras que una
variable numérica puede adoptar infinidad de valores. '), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))), p([style='font-size: 15pt', title='Pregunta'], '9.- ¿Coincide estrictamente la definición de ese "y" con el "y" en Español? '), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))), p([style='font-size: 15pt', title='Respuesta'], '10.- Considere ahora proposiciones compuestas formadas por dos simples y la palabra "o".
w = Suiza está en Europa o Suiza está en Asia = falso '), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),p([style='font-size: 15pt', title='Respuesta'], 's = El gato es un reptil o el gato es un pez = falso ____ '), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),p([style='font-size: 15pt', title='Respuesta'], 't = El maíz es un vegetal o el maíz es comestible = verdad ____ '), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),p([style='font-size: 15pt', title='Pregunta'], 'Un banco dará crédito al Sr. Sutano cuando sea verdadero que:
r = El Sr Sutano es solvente o el Sr. Sutano es amigo del gerente = ___
¿Cuándo se da crédito al Sr. Sutano?
A partir de esos ejemplos, dadas dos proposiciones p y q cualesquiera ¿cuando se diría que p ó q es
verdadera? '), p(div(class='col-xs-11 col-sm-11 col-md-11 col-lg-11', html(\['<hr></hr>']))),
	    \['<br></br>'] ])).



otro -->
	html(
	   [

	    form([style='align: left; margin: 0px 0px 0px 100px;',action='javascript:history.back();', method='POST'], [
	    \['<br></br>'],
	    p([style='font-size: 15pt', title='Pregunta'], '8.- Definir con una expresión formal los siguientes conjuntos: '),
	    p([style='font-size: 16pt', title='respuesta'], 'a. Números enteros entre -6 y + 50 (incluidos ambos):A={x|(-6<=x)y (x<=50) y x E Z'),
	    p([style='font-size: 15pt', title='Respuesta'], 'b. Números enteros divisibles por 3: B={y|(y e Z) ^ (y/3 e Z) ^ mod 3=0'),
	    p([style='font-size: 16pt', title='Pregunta'], 'c. Números fraccionarios entre 2/3 y 1 _______'),
	p([style='font-size: 16pt', title='Pregunta'], 'd. Puntos del plano cartesiano que están a distancia 5 del origen _______'),
		     p([style='font-size: 16pt', title='Pregunta'], 'e. Alumnos de la ULA que aprobaron más de 10 materias: _______'),
		     p([style='font-size: 16pt', title='Pregunta'], 'f. Proposiciones que considera la lógica formal (son verdaderas o falsas): _______'),
		   p([style='font-size: 16pt', title='Pregunta'], '9.- Se dice que B es un subconjunto de A si todo elemento de B lo es de A. Se indica B ⊂ A. Es decir,
9a) B⊂A↔(x ∈ B→x∈ A).
¿Es cierto que A ⊂ A? __ cierto___ ¿Es cierto que B ⊂ A ↔ x ∉ A → x ∉ B? __si___ Haga las tablas de verdad de'),
  table([tr([td(['A c A  ']),html(\['</td>']),td(['<->']),html(\['</td>']),td(['(x e A-> x e A']),html(\['</td></tr>']),tr([td(['verdad']),html(\['</td>']),td(['verdad']),html(\['</td>']),td(['verdad']),html(\['</td></tr>']),tr([td(['falso']),html(\['</td>']),td(['falso']),html(\['</td>']),td(['verdad']),html(\['</td></tr>'])])])]),tr([td(['falso']),html(\['</td>']),td(['verdad']),html(\['</td>']),td(['verdad']),html(\['</td></tr>']),tr([td(['verdad']),html(\['</td>']),td(['falso']),html(\['</td>']),td(['falso']),html(\['</td></tr>'])])])]), p([style='font-size: 16pt', title='Pregunta'], '10.- Dos conjuntos se dicen iguales si tienen los mismos elementos.
10a) Si A ⊂ B y B ⊂ A resulta: A _____ B
¿Porqué? _______'), p([style='font-size: 16pt', title='Pregunta'], '11.- Se pueden considerar como axiomas que afirman la existencia de los nuevos conjuntos. Si A y B son
conjuntos se puede formar un nuevo conjunto Z que los contiene como elementos Z = { _____ , _____ }
¿Se puede decir que los elementos de A también son elementos de Z? _____'),
	 p([style='font-size: 16pt', title='Pregunta'], '12.- Unión. Sean A y B dos conjuntos. Se llama unión de A y B y se indica A B ∪ al conjunto que tiene los
elementos que están en A o en B o en ambos y sólo dichos elementos.
Así si A = {a, b, m, n, p} B = {a, b, s, t, p} entonces A ∪ B = {'),

		      p([style='font-size: 16pt', title='Pregunta'], '14. Intersección. Dados A y B. Se llama intersección al conjunto que tiene sólo los elementos que pertenecen
a A y B. Se indica A ∩ B . Para los conjuntos A y B del caso anterior se tiene: A ∩ B = {
}
'),
	 p([style='font-size: 16pt', title='Respuesta'], '15. Ambas definiciones pueden ponerse formalmente así:
15a) A ∪ B = {x | x ∈ _________A) v (x e B)________________ }
15b) A ∩ B = {x | x ∈ __________A) ^  (x e B)__________________ }'),
	    p(div(class='form-group col-xs-5 col-sm-5 col-md-5 col-lg-5',
	    input([name=submit, type=submit, class='btn btn-md btn-success btn-block', value='Volver'])))])



	    ]).
?- servidor(8007).























