# consulta-cadastro-endPoint
foi criado EndPoint simples Java/Spring
Criando endPoint/Spring 

- projeto MAVEN/JAVA(SPRINGBOOT - ultima Versão)
	-Group - expertostech
	-Artifact - tutorial-rest-api
	-Description - tutorial-rest-api
	-Package name - expertostech.tutorial.rest.api
-
	packaging - jar
	java - 11
...........................................
	dependencias
	- Spring Web
	- Lombok
............
	
...............................UTILIZEI o INTELJ

Deixar o projeto existente
	- File/New/Module from Existing Sources... 
	- na pasta Projeto, selecione e clique seguir.
		- import module from external model/ Maven - Finish
.......................................................................
Vamos adicionar ao nosso projeto essas duas dependências:
<!--junit-->
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
		</dependency>

		<!--mockito-->
		<dependency>
			<groupId>org.mockito</groupId>
			<artifactId>mockito-core</artifactId>
		</dependency>
........................................................................
Feito isso, vamos criar a nossa UsuarioController da seguinte forma:
Agora que já sabemos o que o nosso endpoint tem que fazer , vou criar de fato a funcionalidade:


package consulta.endpoint.consultadados;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Arrays;
import java.util.List;

@RestController
@RequestMapping("usuario")
public class UsuarioController {

    @GetMapping
    public List<Usuario> listaUsuario(){
        return Arrays.asList(Usuario.builder().
                nome("Carlos Eduardo")
                .email("carlospires.edu@gmail.com")
                .idade(35).build());
    }
}


................................................................
 criar o teste do controller:

package cadastro.endpoints.endpoint.controller;

import org.junit.Test;
import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.result.MockMvcResultHandlers;
import org.springframework.test.web.servlet.result.MockMvcResultMatchers;

@WebMvcTest(UsuarioController.class)
public class UsuarioControllerTests {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void testarListaUsuario() throws Exception{
        this.mockMvc.perform(MockMvcRequestBuilders.get("/usuario"))
                .andDo(MockMvcResultHandlers.print())
                .andExpect(MockMvcResultMatchers.jsonPath("$").isArray());
    }
}
...................................................................
criar classe Usuario

package consulta.endpoint.consultadados;

import lombok.Builder;
import lombok.Data;

@Data
@Builder
public class Usuario {
    private String nome;
    private String email;
    private int idade;
}
...................................................................

Criar classe UsuarioService

package consulta.endpoint.consultadados;

import org.springframework.stereotype.Service;

@Service
public class UsuarioService {
    public boolean verificamaioridade(int idade){
        return idade >= 18 ? true:false;
    }
}
