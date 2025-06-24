# produto-api
Proposta de projeto bem simples (explicando tudo):
Nome: produtos-api
Funcionalidades:

GET /produtos → Retorna lista de produtos

POST /produtos → Cadastra um produto e simula envio para uma fila de mensageria


Produto.java

package com.example.produtos;

public class Produto {
    private String nome;
    private Double preco;

    // Construtores
    public Produto() {}
    public Produto(String nome, Double preco) {
        this.nome = nome;
        this.preco = preco;
    }

    // Getters e setters
    public String getNome() { return nome; }
    public void setNome(String nome) { this.nome = nome; }

    public Double getPreco() { return preco; }
    public void setPreco(Double preco) { this.preco = preco; }
}


ProdutoController.java

package com.example.produtos;

import org.springframework.web.bind.annotation.*;
import java.util.ArrayList;
import java.util.List;

@RestController
@RequestMapping("/produtos")
public class ProdutoController {

    List<Produto> produtos = new ArrayList<>();

    @GetMapping
    public List<Produto> listar() {
        return produtos;
    }

    @PostMapping
    public String cadastrar(@RequestBody Produto produto) {
        produtos.add(produto);
        // Simula envio para mensageria
        System.out.println("Mensagem enviada para a fila: Produto cadastrado: " + produto.getNome());
        return "Produto cadastrado com sucesso!";
    }
}



ProdutosApplication.java

package com.example.produtos;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ProdutosApplication {
    public static void main(String[] args) {
        SpringApplication.run(ProdutosApplication.class, args);
    }
}


application.properties (opcional, para ver logs bonitinhos)

spring.application.name=produtos-api
server.port=8080


Teste com Postman:
GET http://localhost:8080/produtos

POST http://localhost:8080/produtos

{
  "nome": "Camisa",
  "preco": 59.9
}


Resumo para você falar na prova:

"Criei uma API simples com Spring Boot para cadastrar produtos. Quando um produto é cadastrado, eu simulo o envio da mensagem para uma fila de mensageria imprimindo no console. Isso representa um sistema desacoplado onde o cadastro envia dados para serem processados em outro momento."
E no console:
Mensagem enviada para a fila: Produto cadastrado: Camisa