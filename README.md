# Painel de Acompanhamento Escolar

**Disciplina:** Projeto Integrado - Entregável Parcial 2  
**Curso:** Análise e Desenvolvimento de Sistemas (UFCA)  
**Estudantes:** Antonio Alex Dayson Tomaz e Maria Alexsandra Tomaz

---

## 📌 Visão Geral

Este projeto é um sistema de gestão acadêmica desenvolvido em Python, focado em simplicidade e robustez. Ele permite gerenciar todo o ciclo escolar: desde o cadastro de alunos, professores e responsáveis, até a organização de turmas, lançamento de notas, controle de frequência e geração de boletins.

Nosso objetivo foi criar um código limpo, fácil de entender e que utilize boas práticas de engenharia de software, separando as regras de negócio (domínio) da persistência de dados (banco de dados).

---

## 🚀 Possíveis usos da nossa solução
*(Componente Extensionista)*

A equipe compreendeu que o Componente Extensionista é o pilar que valida a utilidade social do software. Por isso, criamos no README.md a seção obrigatória "Possíveis usos da nossa solução", onde conectamos cada funcionalidade técnica a uma dor real da comunidade ou de pequenos negócios.
Abaixo, aprofundamos os três cenários identificados, justificando como o sistema resolve problemas específicos:

### 1. Profissionalização de Escolas de Pequeno Porte e Cursos Livres
Muitas escolas de ensino básico, de idiomas, música ou artes na região do Cariri ainda dependem de processos manuais ou planilhas isoladas que geram perda de histórico e erros de cálculo.
*   **Impacto Real:** Nossa solução permite a transição do físico para o digital sem a necessidade de investimentos em softwares caros e complexos.
*   **Solução de Problema:** A automação do cálculo de médias ponderadas e o controle centralizado de matrículas eliminam erros humanos, garantindo que o boletim entregue ao aluno seja matematicamente preciso e confiável.

### 2. Sustentabilidade e Transparência em ONGs e Projetos Sociais
Instituições que oferecem reforço escolar ou atividades socioeducativas dependem frequentemente de doações e parcerias que exigem prestação de contas rigorosa.
*   **Impacto Real:** O sistema atua como uma ferramenta de gestão de impacto social.
*   **Solução de Problema:** O extrato de frequência detalhado por período e disciplina permite que a ONG comprove a assiduidade dos beneficiários aos seus financiadores. A capacidade de registrar faltas justificadas com motivos (ex: atestados) profissionaliza o atendimento social e ajuda a identificar causas de evasão escolar prematuramente.

### 3. Escalabilidade em Centros de Treinamento Corporativo
Pequenas empresas que investem na capacitação de funcionários precisam monitorar se o treinamento está gerando resultados práticos.
*   **Impacto Real:** O sistema organiza o capital humano através do acompanhamento de competências.
*   **Solução de Problema:** Ao tratar cada "treinamento" como uma disciplina e cada "avaliação" como um teste de competência, o RH pode identificar rapidamente funcionários que atingiram a média de aprovação e estão aptos para novas funções, centralizando o histórico de desenvolvimento profissional em um único banco de dados seguro.

### 4. Dimensão da Inclusão Digital
Ao optarmos por uma solução leve em Python e SQLite, garantimos que o software possa rodar em computadores com recursos limitados, facilitando a inclusão digital de entidades que não possuem acesso a servidores de alta performance ou conexão constante com a internet.

---

## 🧩 Identificação dos Princípios de POO

Utilizamos a Programação Orientada a Objetos para tornar o código mais próximo do mundo real. Abaixo, detalhamos como cada princípio foi aplicado no projeto:

### 1. Encapsulamento
Protegemos os dados internos dos objetos para evitar estados inconsistentes.
*   **No código:** Na classe `Student` (`src/domain/models.py`), o método construtor `__init__` valida o email e a matrícula antes de criar o objeto. Se um email inválido for passado, o objeto nem chega a ser criado, garantindo a integridade do sistema.

### 2. Abstração
Simplificamos entidades complexas do mundo real em classes claras e focadas.
*   **No código:** Criamos classes como `Student`, `Teacher` e `Parent`. Embora uma pessoa real tenha milhares de características, para o sistema abstraímos apenas o necessário: nome, ID e status ativo, ignorando detalhes irrelevantes como cor dos olhos ou altura.

### 3. Composição
Construímos objetos complexos combinando objetos mais simples.
*   **No código:** A classe `Student` possui uma lista `self.parents`. Isso modela a relação "um aluno TEM responsáveis". Não usamos herança aqui, mas sim composição, permitindo que um aluno tenha múltiplos responsáveis vinculados a ele dinamicamente.

---

## 💻 Como usar (Exemplos)

O sistema é operado através de "Serviços" que orquestram as regras de negócio. Veja exemplos práticos:

### Exemplo 1: Matriculando um aluno
Utilizamos a classe `ServicosSecretaria` para garantir que apenas alunos ativos sejam matriculados.

```python
# Exemplo conceitual de uso
secretaria = ServicosSecretaria(repo_alunos, repo_turmas, repo_pais)

# O metodo verifica se o aluno existe e está ativo antes de vincular
secretaria.matricular_aluno(student_id=101, classroom_id=5, academic_year=2024)
```

### Exemplo 2: Lançando notas
A classe `ServicosDoAluno` impede notas duplicadas para a mesma avaliação.

```python
# O sistema lança a nota e registra quem avaliou e quando
servico_aluno.lancar_nota(
    student_id=101, 
    assessment_id=20, 
    score=8.5, 
    graded_by="Prof. Silva"
)
```

---

## ⚙️ Processos de Software Adotados

Para garantir a qualidade e a manutenção do software, adotamos processos de engenharia bem definidos:

1.  **Arquitetura em Camadas:** O projeto não é um "script único". Ele é dividido em:
    *   **Domain (Domínio):** Onde vivem as regras essenciais (ex: validação de nota).
    *   **Application (Aplicação):** Onde estão os serviços que o usuário usa (ex: gerar boletim).
    *   **Infrastructure (Infraestrutura):** Onde lidamos com detalhes técnicos como o banco de dados SQL.
    *   Isso permite trocar o banco de dados no futuro sem quebrar as regras de negócio.

2.  **Desenvolvimento Orientado a Testes (TDD - Inserção):** Embora o foco seja o projeto final, a estrutura de testes na pasta `tests/` garante que cada nova funcionalidade (como a validação de CPF) seja verificada automaticamente antes de ser considerada "pronta".

---

## 🌟 O que é o "Projeto Físico" de um Banco de Dados?
*(Componente Extensionista — Para estudantes e comunidade)*

Podemos comparar a cosntrução de um banco de dados à construção de uma casa:

O **Projeto Lógico** é a Planta Baixa: É o desenho conceitual onde decidimos que a casa terá sala, quartos e cozinha. É onde definimos as relações entre as "peças" (ex: o quarto deve ter acesso ao corredor).

O **Projeto Físico** é a Obra Real: É o momento de "sujar as mãos" e decidir os materiais. Vamos usar tijolo ou concreto? Qual a espessura exata dos canos para não haver vazamento? Como as trancas das portas serão instaladas?.

## 🛠️ Traduzindo para o Código
No desenvolvimento de software, o projeto físico é a tradução dos nossos diagramas para comandos reais de SQL (Structured Query Language) que o computador consegue executar. Neste sistema, implementamos o projeto físico manualmente em SQLite 3.0+, sem usar ferramentas automáticas (ORMs), para garantir controle total sobre a fundação dos dados.

**Este processo define detalhes vitais como:**

**Tipagem de Dados:** Garantir que datas sigam o padrão internacional ISO-8601 e que notas sejam números reais precisos.

**Vínculos Seguros:** O uso de Chaves Estrangeiras (Foreign Keys) para criar elos inquebráveis entre alunos, professores e responsáveis.

**Trancas de Segurança (Constraints):** São as regras de ouro. Se o código Python falhar e tentar salvar uma nota "11" ou um CPF inválido, o banco de dados bloqueia a ação.

## 💡 Por que isso é importante para o programador?
O banco de dados é a "última linha de defesa" de um sistema. Um projeto físico bem estruturado garante que, mesmo após anos de uso ou erros inesperados na interface, as informações da escola continuem íntegras, organizadas e protegidas. Aprender a construir essa base manualmente é o que diferencia um programador comum de um desenvolvedor que realmente entende como os dados sobrevivem ao tempo.

## 🏗️ Detalhamento do Projeto Físico

O banco de dados foi estruturado manualmente em **SQLite 3.0+**, utilizando SQL explícito (sem bibliotecas automáticas/ORM) para garantir total controle sobre a integridade acadêmica.

### 1. Tabelas e Tipos de Dados
Implementamos **11 tabelas** organizadas para evitar repetição de informação (Normalização):

- **Atores (students, teachers, parents):** Usam identificadores únicos (`INTEGER PRIMARY KEY AUTOINCREMENT`) para rapidez e facilidade de consulta manual.
- **Datas:** Armazenadas como strings no formato **ISO-8601 (YYYY-MM-DD)** para garantir que as buscas por período funcionem em qualquer sistema.
- **Notas e Pesos:** Definidos como `REAL`/`DECIMAL` para permitir cálculos matemáticos precisos de média ponderada.

### 2. Chaves e Relacionamentos
**Foreign Keys (Chaves Estrangeiras):** Criam os "vínculos" entre tabelas.

- **ON DELETE CASCADE:** Aplicado em vínculos familiares e de frequência. Se um aluno é removido, o sistema apaga automaticamente seus vínculos, evitando "lixo" no banco.
- **ON DELETE RESTRICT:** Aplicado em turmas e notas. O sistema impede a exclusão de uma turma se houver alunos matriculados nela, preservando o histórico escolar.

### 3. Restrições (Constraints) - A Proteção dos Dados
O projeto utiliza **18 restrições de verificação (CHECK)** e **11 de unicidade (UNIQUE)**:

- **Notas:** Uma regra impede que qualquer nota seja menor que 0 ou maior que 10.
- **Documentos:** O campo de CPF e Email exige formatos válidos e impede que dois responsáveis usem o mesmo CPF.
- **Lógica de Frequência:** Uma restrição impede que um aluno seja marcado como "Presente" e, ao mesmo tempo, possua uma "Justificativa de Falta".

---

## 📂 Estrutura do Projeto

Mantivemos uma estrutura organizada para facilitar a navegação:

```
projeto/
├── main.py                     # Script principal de demonstração (Ponto de entrada)
├── DESCRICAO_DO_PROJETO.md     # Detalhes técnicos completos
├── src/
│   ├── domain/models.py        # As classes (Aluno, Professor, Nota...)
│   ├── application/services.py # As regras (Cálculo de média, Matrícula...)
│   └── infrastructure/         # Onde o SQL vive
│       ├── database.py         # Código Python que fala com o banco
│       └── schema.sql          # O script de criação do banco físico
└── tests/                      # Testes automatizados para garantir qualidade
```

---

## 🚀 Como Executar o Projeto

Para testar nosso sistema, siga os passos abaixo no terminal:

1. **Prepare o ambiente:**
   ```bash
   python -m venv .venv
   .venv\Scripts\activate   # No Windows
   pip install -r requirements.txt
   ```

2. **Rode a demonstração completa:**
   O arquivo `main.py` cria um cenário real: cadastra alunos, turmas, lança notas e gera boletins.
   ```bash
   python main.py
   ```

3. **Verifique os testes:**
   Cobrimos o sistema com 60 testes automatizados para garantir que tudo funciona.
   ```bash
   pytest tests/ -v
   ```

---

## 🛠️ Tecnologias Utilizadas

- **Python 3.12**
- **SQLite**
- **pytest**

---
*Este projeto foi desenvolvido para a disciplina de Projeto Integrado 2 do Curso de Análise e Desenvolvimento de Sistemas da UFCA.*
