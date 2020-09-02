import java.io.File;
import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.parsers.ParserConfigurationException;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerException;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
 
import org.w3c.dom.Attr;
import org.w3c.dom.Document;
import org.w3c.dom.Element;
 
public class WriteXMLFile {
 
	public static void main(String argv[]) {
 
	  try {
 
		DocumentBuilderFactory docFactory = DocumentBuilderFactory.newInstance();
		DocumentBuilder docBuilder = docFactory.newDocumentBuilder();
 
		// elemento raiz
		Document doc = docBuilder.newDocument();
		Element rootElement = doc.createElement("Informacion");
		doc.appendChild(rootElement);
 
		// ciudadano
		Element ciudadano = doc.createElement("ciudadano");
		rootElement.appendChild(ciudadano);
 
		// atributo del elemento ciudadano
		Attr attr = doc.createAttribute("id");
		attr.setValue("1");
		ciudadano.setAttributeNode(attr);
 
		// NOMBRE
		Element nombre = doc.createElement("nombre");
		nombre.appendChild(doc.createTextNode("Heredia Mendez Alejandra"));
		ciudadano.appendChild(nombre);
 
		// DOMICILIO
		Element domicilio = doc.createElement("domicilio");
		domicilio.appendChild(doc.createTextNode("Barr de Jesús Tlatempa 72760 San Pedro Cholula, Pue"));
		ciudadano.appendChild(domicilio);
 
		// CURP
		Element curp = doc.createElement("curp");
		curp.appendChild(doc.createTextNode("HEMA971129MVZRNL02"));
		ciudadano.appendChild(curp);

        // FECHA NACIMIENTO
		Element fnaci = doc.createElement("fnaci");
		fnaci.appendChild(doc.createTextNode("29/11/1997"));
		ciudadano.appendChild(fnaci);

 
		TransformerFactory transformerFactory = TransformerFactory.newInstance();
		Transformer transformer = transformerFactory.newTransformer();
		DOMSource source = new DOMSource(doc);
		StreamResult result = new StreamResult(new File("C:\\archivo.xml"));
 
 
		transformer.transform(source, result);
 
		System.out.println("Archivo guardado");
 
		} catch (ParserConfigurationException pce) {
			pce.printStackTrace();
		} catch (TransformerException tfe) {
			tfe.printStackTrace();
		}
	}
}