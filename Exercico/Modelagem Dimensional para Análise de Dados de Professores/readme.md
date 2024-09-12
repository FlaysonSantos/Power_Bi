
---
# Titulo: Modelagem Dimensional para Análise de Dados de Professores
## Desenvolvido por: [Flayson Santos](https://github.com/FlaysonSantos)'
---

# Modelagem Dimensional para Análise de Dados de Professores
### Desenvolvido por [Flayson Santos](https://github.com/FlaysonSantos)

---

# Objetivo da Atividade

- Criar um diagrama dimensional utilizando o modelo de Star Schema.
- Foco na análise de dados relacionados aos professores.
- A Tabela Fato deve refletir os dados de professores, cursos ministrados, e departamentos.
- Estruturar as tabelas de dimensão que fornecem o contexto para a Tabela Fato.

---

# Tabelas de Dimensão

- **Dim_Professor**: Informações sobre os professores.
- **Dim_Departamento**: Informações sobre os departamentos.
- **Dim_Curso**: Informações sobre os cursos ministrados.
- **Dim_Disciplina**: Detalhes das disciplinas ofertadas.
- **Dim_Data**: Dimensão de datas para análises temporais.

---

# Tabela Fato

- **Fato_Professor**: Tabela central do esquema que conecta as dimensões.
- Contém métricas como:
  - Quantidade de alunos.
  - Quantidade de matriculados.
  - Carga horária.

---
# Star Schema
![Schema](https://github.com/FlaysonSantos/Power_Bi/blob/main/Exercico/Modelagem%20Dimensional%20para%20An%C3%A1lise%20de%20Dados%20de%20Professores/schema.jpg)

# Código SQL - Criação das Tabelas de Dimensão

```sql
CREATE TABLE Dim_Professor (
    idProfessor INT PRIMARY KEY,
    Nome VARCHAR(255),
    idDepartamento INT,
    Coordenador BOOLEAN,
    FOREIGN KEY (idDepartamento) REFERENCES Dim_Departamento(idDepartamento)
);

CREATE TABLE Dim_Departamento (
    idDepartamento INT PRIMARY KEY,
    Nome_Departamento VARCHAR(255),
    idProfessor_Coordenador INT,
    FOREIGN KEY (idProfessor_Coordenador) REFERENCES Dim_Professor(idProfessor)
);
...
```

---

# Código SQL - Criação da Tabela Fato

```sql
CREATE TABLE Fato_Professor (
    idProfessor INT,
    idCurso INT,
    idDisciplina INT,
    DataID INT,
    Quantidade_Alunos INT,
    Quantidade_Matriculados INT,
    Carga_Horaria INT,
    PRIMARY KEY (idProfessor, idCurso, idDisciplina, DataID),
    FOREIGN KEY (idProfessor) REFERENCES Dim_Professor(idProfessor),
    FOREIGN KEY (idCurso) REFERENCES Dim_Curso(idCurso),
    FOREIGN KEY (idDisciplina) REFERENCES Dim_Disciplina(idDisciplina),
    FOREIGN KEY (DataID) REFERENCES Dim_Data(DataID)
);
```

---

# Conclusão

- O modelo dimensional permite uma análise eficiente dos dados dos professores.
- O esquema em estrela facilita consultas rápidas e agregações.
- A modelagem garante integridade referencial e consistência de dados.

Obrigado pela atenção!
