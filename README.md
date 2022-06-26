<div align="center">
<table>
    <theader>
        <tr>
            <td><img src="https://github.com/rescobedoq/pw2/blob/main/epis.png?raw=true" alt="EPIS" style="width:50%; height:auto"/></td>
            <th>
                <span style="font-weight:bold;">UNIVERSIDAD NACIONAL DE SAN AGUSTIN</span><br />
                <span style="font-weight:bold;">FACULTAD DE INGENIERÍA DE PRODUCCIÓN Y SERVICIOS</span><br />
                <span style="font-weight:bold;">DEPARTAMENTO ACADÉMICO DE INGENIERÍA DE SISTEMAS E INFORMÁTICA</span><br />
                <span style="font-weight:bold;">ESCUELA PROFESIONAL DE INGENIERÍA DE SISTEMAS</span>
            </th>
            <td><img src="https://github.com/rescobedoq/pw2/blob/main/abet.png?raw=true" alt="ABET" style="width:50%; height:auto"/></td>
        </tr>
    </theader>
    <tbody>
        <tr><td colspan="3"><span style="font-weight:bold;">Formato</span>: INFORME DE LABORATORIO</td></tr>
        <tr><td><span style="font-weight:bold;">Aprobación</span>:  2022/03/01</td><td><span style="font-weight:bold;">Código</span>: GUIA-PRLD-001</td><td><span style="font-weight:bold;">Página</span>: 1</td></tr>
    </tbody>
</table>
</div>
<div align="center">
<span style="font-weight:bold;">GUÍA DE LABORATORIO</span><br />
</div>

<table>
<theader>
<tr><th colspan="6">INFORMACIÓN BÁSICA</th></tr>
</theader>
<tbody>
<tr><td>ASIGNATURA:</td><td colspan="5">Estructura de Datos y Algoritmos</td></tr>
<tr><td>TÍTULO DE LA PRÁCTICA:</td><td colspan="5">Arboles</td></tr>
<tr>
<td>NÚMERO DE PRÁCTICA:</td><td>05</td><td>AÑO LECTIVO:</td><td>2022 A</td><td>NRO. SEMESTRE:</td><td>III</td>
</tr>
<tr>
<td>FECHA INICIO::</td><td>23-Jun-2022</td><td>FECHA FIN:</td><td>30-Jun-2022</td><td>DURACIÓN:</td><td>02 horas</td>
</tr>
<tr><td colspan="6">RECURSOS:
</td>
</<tr>
  <tr><td colspan="6">ALUMNO:
<ul>
<li>Frank's Vilca Quispe - fvilcaqui@unsa.edu.pe</li>
</ul>
</td>
</<tr>
<tr><td colspan="6">DOCENTES:
<ul>
<li>Richart Smith Escobedo Quispe - rescobedoq@unsa.edu.pe</li>
</ul>
</td>
</<tr>
</tdbody>
</table>

#
   ## SOLUCION Y RESULTADOS
#

## I. SOLUCION DE EJERCICIOS/PROBLEMAS
   Ejercicio 1:
     Corchetes equilibrados:
    -Para resolver este ejercicio lo primero que hice fue crear un metodo el cual separaria los caracteres de mi cadena y los guardaria en un 
     ArrayList.
     
     public static void Convertir(String a,ArrayList<String> Array) {
		for(int i=0;i<a.length();i++) {
			char letra = a.charAt(i); //Separara los caracteres
			String nuevo = String.valueOf(letra);
			Array.add(nuevo);  //los envio los caracteres al Array 
		}
	}

      -El siguiente metodo es isBalanced el cual se encargara de verificar si esta balanceado o no.
      public static String isBalanced(ArrayList<String> Array) {
		String a="";
		String b="";
		String resp = "";
		if(Array.size()%2 != 0) {
			return "no";  //Si los datos no son pares significa que no son balanceados por lo que enviara un no
		}
		for(int i=0,j=Array.size()-1;i<Array.size()/2;i++,j--) {
			a = Array.get(i);
			b = Array.get(j); //Verificamos que sean iguales para enviar que son iguales
			if((a.equals("(")&&b.equals(")"))||(a.equals("[")&&b.equals("]"))||(a.equals("{")&&b.equals("}"))) {
				resp = "si";
			}else {
				resp = "no";
				break;
			}
		}
		return resp;
	}
	
	Resultados:
	
	Ejemplo de si:
![image](https://user-images.githubusercontent.com/87882802/175794285-c6201a83-8f10-4152-b9d7-f2edf1bcd2e8.png)
![image](https://user-images.githubusercontent.com/87882802/175794296-2e84855b-c29d-4ca6-900e-af5455231eae.png)
	
	Ejemplo de no:
![image](https://user-images.githubusercontent.com/87882802/175794303-b527d808-3985-471e-99f1-036f3c95848f.png)
![image](https://user-images.githubusercontent.com/87882802/175794305-7ea63608-ad78-44c4-af9a-8fb2687b397f.png)


	
   Ejercicio 2:
     Operaciones de arbol AVL:
   
   Ejercicio 3:
     Arbol AVL:
     //Iniciaremos los datos
     lass Node{
		protected E data;
		protected Node left;
		protected Node right;
		protected int fb;
		
		public Node(E data, Node left, Node right) {
			this.data = data;
			this.left = left;
			this.right = right;
			this.fb = 0;
		}
		public Node(E data) {
			this(data, null, null);
		}
	}
	private Node root;
	private boolean height;
	
	public AVL() {
		this.root = null;
	}
	//Para ve si el arbol esta vacio
	public boolean isEmpty() {
		return this.root == null;
	}
	//Servira pra insertar nodos
	public void insert (E x) throws ItemDuplicated {
		this.height = false;
		this.root = insertRec(x, this.root);
	}
	//Insertara nodos y los ordenara de forma AVL
	private Node insertRec(E x,Node current) throws ItemDuplicated{
		Node res = current;
		if(current == null) {
			this.height = true;
			res = new Node(x);
		}	
		else {
			int resC = current.data.compareTo(x);
			if(resC == 0)
				throw new ItemDuplicated("El dato " + x + "Ya fue insertado a ");
			if(resC < 0) {
				res.right = insertRec(x, current.right);
				if (this.height) {
					switch(res.fb) {
					case -1 : res.fb = 0; this.height = false; break;
					case 0 : res.fb = 1; this.height = true; break;
					case 1 : //res.fb = 2;
					           res = balanceToLeft(res);
					           this.height = false;
					}
				}
			}
			else {
				res.left = insertRec(x, current.left);
			}
		}	
		return res;
	}
	//Balancearemos para la izquierda
	private Node balanceToLeft(Node node) {
		Node son = node.right;
		switch(son.fb) {
		case 1 : node.fb = 0;
		         son.fb = 0;  
			     node = rotateSL(node); 
			     break;
		case -1: Node grandson = son.left;
		         switch(grandson.fb) {
		         case -1 : node.fb = 0; son.fb = -1; break;
		         case 0 : node.fb = 0; son.fb = 0; break;
		         case 1 : node.fb = 1; son.fb = 0; break;
		         }
		         grandson.fb = 0;
		         node.right = rotateSR(son);
		         node = rotateSL(node);
		         break;
		}
		return node;
	}
	//rotaremos para la izquierda
	private Node rotateSL(Node node) {
		Node son = node.right;
		node.right = son.left;
		son.left = node;
		node = son;
		return node;
	}
	//rotaremos para la derecha
	private Node rotateSR(Node node) {
		Node son = node.left;
		node.left = son.right;
		son.right = node;
		node = son;
		return node;
	}
	
	public String toString() {
		if (isEmpty())
			return"Arbol vacio... ";
		return postOrden(this.root);
	}
	
	private String postOrden(Node current) {
		String str = "";
		if(current.left != null) str += postOrden(current.left);
		str += current.data + "[" + current.fb +"], ";
		if(current.right != null) str += postOrden(current.right);
		return str;
	}
     
     Resultados:
 ![image](https://user-images.githubusercontent.com/87882802/175794361-b76d93b0-ac31-4efb-a7dc-853a42dc4f84.png)

#

   ## BIBLIOGRAFIA
    - https://www.w3schools.com/java/
    - https://www.eclipse.org/downloads/packages/release/2022-03/r/eclipse-ide-enterprise-java-and-web-developers
    - https://algorithmtutor.com/Data-Structures/Tree/AVL-Trees/
    - https://docs.oracle.com/javase/tutorial/java/generics/types.html
   
#
