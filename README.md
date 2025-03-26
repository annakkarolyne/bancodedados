# banco de dados
#mySQL
 Criando o banco de dados
CREATE DATABASE Escola;
USE Escola;

-- Criando as tabelas
CREATE TABLE Alunos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE NOT NULL,
    email VARCHAR(100) NOT NULL
);

CREATE TABLE Professores (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL
);

CREATE TABLE Disciplinas (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    id_professor INT,
    FOREIGN KEY (id_professor) REFERENCES Professores(id)
);

CREATE TABLE Matriculas (
    id_aluno INT,
    id_disciplina INT,
    ano INT NOT NULL,
    PRIMARY KEY (id_aluno, id_disciplina, ano),
    FOREIGN KEY (id_aluno) REFERENCES Alunos(id),
    FOREIGN KEY (id_disciplina) REFERENCES Disciplinas(id)
);

-- Inserindo dados
INSERT INTO Professores (nome, email) VALUES ('Carlos Silva', 'carlos@email.com'), ('Ana Souza', 'ana@email.com'), ('Pedro Lima', 'pedro@email.com');

INSERT INTO Disciplinas (nome, id_professor) VALUES ('Matemática', 1), ('Português', 2), ('História', 3), ('Ciências', 1);

INSERT INTO Alunos (nome, data_nascimento, email) VALUES 
    ('João Oliveira', '2005-03-10', 'joao@email.com'),
    ('Maria Santos', '2004-07-21', 'maria@email.com'),
    ('Lucas Mendes', '2003-11-30', 'lucas@email.com'),
    ('Carla Ferreira', '2006-01-15', 'carla@email.com'),
    ('Roberta Lima', '2002-09-25', 'roberta@email.com');

INSERT INTO Matriculas (id_aluno, id_disciplina, ano) VALUES (1, 1, 2024), (1, 2, 2024), (2, 2, 2024), (3, 3, 2024), (4, 4, 2024);

-- Consultas e manipulação de dados
SELECT * FROM Alunos;
SELECT nome FROM Professores;
SELECT * FROM Disciplinas ORDER BY nome;
UPDATE Alunos SET email='novoemail@email.com' WHERE id=1;
SELECT * FROM Alunos WHERE YEAR(data_nascimento) > 2000;
SELECT Disciplinas.nome, Professores.nome FROM Disciplinas INNER JOIN Professores ON Disciplinas.id_professor = Professores.id;
SELECT DISTINCT nome FROM Professores;
SELECT * FROM Matriculas WHERE ano = 2024;
SELECT * FROM Matriculas ORDER BY id_aluno;
SELECT id_disciplina, COUNT(id_aluno) FROM Matriculas GROUP BY id_disciplina;
SELECT id_disciplina FROM Matriculas GROUP BY id_disciplina HAVING COUNT(id_aluno) > 2;
SELECT id_disciplina FROM Matriculas GROUP BY id_disciplina HAVING COUNT(id_aluno) < 3;
SELECT * FROM Alunos WHERE id NOT IN (SELECT id_aluno FROM Matriculas);
SELECT nome FROM Professores WHERE id NOT IN (SELECT id_professor FROM Disciplinas);
DELETE FROM Alunos WHERE id=5;
DELETE FROM Matriculas WHERE id_disciplina=2;
