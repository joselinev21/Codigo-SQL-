Código fuente de SQL para la creación del modelo físico  (DDL) que incluya el código fuente de SQL para el llenado de cada tabla (DML) 
DROP DATABASE IF EXISTS FEI;
CREATE DATABASE FEI;
USE fei;
CREATE TABLE alumno (
    matricula VARCHAR(10) PRIMARY KEY,
    nombre VARCHAR(30) NOT NULL,
    apaterno VARCHAR(30) NOT NULL,
    amaterno VARCHAR(30) NOT NULL,
    email VARCHAR(60) NOT NULL,
    fecha_nac DATE,
    edad INT
    );
CREATE TABLE grado_estudios (
    id_grado INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(18) NOT NULL
    );
CREATE TABLE profesor (
    num_personal INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    id_grado INT UNSIGNED NOT NULL,
    nombre VARCHAR(30) NOT NULL,
    apaterno VARCHAR(30) NOT NULL,
    amaterno VARCHAR(30) NOT NULL,
    email VARCHAR(30) NOT NULL,
    CONSTRAINT fk_grado_estudios FOREIGN KEY (id_grado)
    REFERENCES grado_estudios (id_grado)
    ON DELETE CASCADE ON UPDATE CASCADE
    );
CREATE TABLE carrera (
    cod_carrera INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(10) NOT NULL,
    descripcion VARCHAR(100) NOT NULL
    );
CREATE TABLE area (
    cod_area INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(30) NOT NULL
    );
CREATE TABLE materia (
    cod_materia INT AUTO_INCREMENT PRIMARY KEY,
    cod_carrera INT NOT NULL,
    cod_area INT NOT NULL,
    nombre VARCHAR(100) NOT NULL,
    descripcion VARCHAR(150) NOT NULL,
    creditos INT NOT NULL,
    bloque INT NOT NULL,
    CONSTRAINT fk_cod_carrera FOREIGN KEY (cod_carrera)
    REFERENCES carrera (cod_carrera)
    ON DELETE CASCADE ON UPDATE CASCADE,
    CONSTRAINT fk_cod_area FOREIGN KEY (cod_area)
    REFERENCES area (cod_area)
    ON DELETE CASCADE ON UPDATE CASCADE
    );
CREATE TABLE periodo (
    cod_periodo INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(40) NOT NULL,
    fecha_inicio DATE NOT NULL,
    fecha_fin DATE NOT NULL
    );
CREATE TABLE oferta (
    nrc INT PRIMARY KEY,
    cod_materia INT NOT NULL,
    cod_periodo INT NOT NULL,
    num_personal INT UNSIGNED NOT NULL,
    CONSTRAINT fk_cod_materia FOREIGN KEY (cod_materia)
    REFERENCES materia (cod_materia)
    ON DELETE CASCADE ON UPDATE CASCADE,
    CONSTRAINT fk_cod_periodo FOREIGN KEY (cod_periodo)
    REFERENCES periodo (cod_periodo)
    ON DELETE CASCADE ON UPDATE CASCADE,
    CONSTRAINT fk_num_personal FOREIGN KEY (num_personal)
    REFERENCES profesor (num_personal)
    ON DELETE CASCADE ON UPDATE CASCADE
    );

CREATE TABLE carga_academica (
    matricula VARCHAR(10),
    nrc INT,
    PRIMARY KEY (matricula, nrc),
    calificacion FLOAT NOT NULL,
    CONSTRAINT fk_matricula FOREIGN KEY (matricula)
    REFERENCES alumno (matricula)
    ON DELETE CASCADE ON UPDATE CASCADE,
    CONSTRAINT fk_nrc FOREIGN KEY (nrc)
    REFERENCES oferta (nrc)
    ON DELETE CASCADE ON UPDATE CASCADE
    );
INSERT INTO alumno VALUES('S19030017', 'Sandra', 'Bustillos', 'Gómez', 'sbustillosg@gmail.com', '2001/02/12', 22);
INSERT INTO alumno VALUES('S23043019', 'Gael', 'Pineda', 'Sánchez', 'gaelpsanchez12@gmail.com', '2005/09/20', 18);
INSERT INTO alumno VALUES('S20123456', 'Angela', 'García', 'Fuentes', 'afuentes33@gmail.com', '2002/05/18', 21);
INSERT INTO alumno VALUES('S21016023', 'Jorge', 'Cortés', 'Perez', 'jorgperez12@gmail.com', '2003/12/07', 20);
INSERT INTO alumno VALUES('S21092393', 'Pineda', 'Ramos', 'gaelp3643@gmail.com', '2000/09/09', 23);
INSERT INTO alumno VALUES('S20030096', 'Carolina', 'Campos', 'Rosiles', 'carros30@gmail.com', '2002/10/09', 22);
INSERT INTO alumno VALUES('S22098096', 'Norma', 'Torales', 'Quintana', 'normaquintana21@gmail.com', '2004/04/17', 19);
INSERT INTO alumno VALUES('S22085094', 'Isaac', 'Ríos', 'Reyes', 'isri255@gmail.com', '2001/07/16', 22);
INSERT INTO alumno VALUES('S20938474', 'María', 'Pizzo', 'Pavón', '9604mp@gmail.com', '2000/06/12', 23);
INSERT INTO periodo VALUES(1, 'Febrero-Julio 2023', '2023/02/07', '2023/06/02');
INSERT INTO periodo VALUES(2, 'Intersemestral Verano', '2023/06/19', '2023/08/08');
INSERT INTO periodo VALUES(3, 'Agosto-Diciembre 2023', '2023/08/21', '2023/12/08');
INSERT INTO periodo VALUES(4, 'Intersemestral Invierno', '2024/01/03', '2024/01/30');
INSERT INTO area VALUES(1, 'Area de formación básica');
INSERT INTO area VALUES(2, 'Iniciación a la disciplina');
INSERT INTO area VALUES(3, 'Disciplinar');
INSERT INTO area VALUES(4, 'Terminal');
INSERT INTO area VALUES(5, 'Elección libre');
INSERT INTO carrera VALUES(1, 'LIS', 'Licenciatura en Ingeniería de Software');
INSERT INTO carrera VALUES(2, 'LICIC', 'Licenciatura en Ingeniería de Ciberseguridad e Infraestructura de Cómputo');
INSERT INTO carrera VALUES(3, 'LISTI', 'Licenciatura en Ingeniería en Sistemas y Tecnologías de la Información');
INSERT INTO carrera VALUES(4, 'LE', 'Licenciatura en Estadística');
INSERT INTO carrera VALUES(5, 'LTC', 'Licenciatura en Tecnologías Computacionales');
INSERT INTO materia VALUES(1, 1, 1, 'Habilidades del pensamiento crítico y creativo', 'Habilidades de Pensamiento Crítico y Creativo pertenece al ÁFBG.', 6, 1);
INSERT INTO materia VALUES(2, 1, 1, 'Computacion básica', 'El estudiante realiza prácticas individuales y grupales empleando herramientas digitales', 6, 1);
INSERT INTO materia VALUES(3, 1, 2, 'Habilidades de comunicación', 'Esta experiencia educativa se encuentra en el área de iniciación a la disciplina, obligatoria.', 6, 2);
INSERT INTO materia VALUES(4, 1, 2, 'Programacón', 'Programación en la carrera de Ingeniería de Software, se localiza en el área de formación disciplinaria.', 8, 2);
INSERT INTO materia VALUES(5, 1, 3, 'Procesos para la ingeniería de software', 'Esta EE se ubica en el área disciplinar (4 hrs. teoría y 2 hrs. prácticas, 10 créditos).', 10, 3 );
INSERT INTO materia VALUES(6, 1, 3, 'Sistemas Operativos', 'La EE tiene como propósito que cubran las necesidades que demanda la sociedad en materia de Ingeniería de Software', 9, 3 );
INSERT INTO materia VALUES(7, 1, 4, 'Experiencia Recepcional', 'La experiencia educativa Experiencia Recepcional está ubicada en el área terminal.', 12, 5);
INSERT INTO materia VALUES(8, 1, 4, 'Servicio Social', 'La experiencia educativa Servicio Social está ubicada en el área terminal, contabilizando un total de 12 créditos.', 12, 6);
INSERT INTO materia VALUES(9, 1, 5, 'Agedrez', 'Eleccion libre', 9, 4);
INSERT INTO materia VALUES(10, 1, 5, 'Natación', 'Eleccion libre', 9, 4);
INSERT INTO materia VALUES(11, 2, 1, 'Literacidad digital', 'Ésta EE planteada como taller pertenece al Área de Formación Básica General, tiene un valor de 4 créditos', 4, 1);
INSERT INTO materia VALUES(12, 2, 1, 'Pensamiento crítico para la solución de problemas', 'Desarrolla las competencias para la formulación de problemas.', 4, 1);
INSERT INTO materia VALUES(13, 2, 2, 'Introducción a ciberseguridad', 'Elementos que intervienen en una estrategia de ciberseguridad', 7, 2);
INSERT INTO materia VALUES(14, 2, 2, 'Probabilidad y Estadística', 'Identifica entre eventos independientes y dependientes para el cálculo de probabilidades.', 8, 2);
INSERT INTO materia VALUES(15, 2, 3, 'Criptografia', 'La criptografía es un elemento fundamental de la protección de la información.', 8, 3);
INSERT INTO materia VALUES(16, 2, 3, 'Computo forense', 'El estudiante realiza una investigación forense digital.', 8, 3);
INSERT INTO materia VALUES(17, 2, 4, 'Computo de alta disponibilidad', 'Soluciones de alta disponibilidad con base en los requerimientos del negocio.', 6, 5);
INSERT INTO materia VALUES(18, 2, 4, 'Acreditación del idioma inglés', 'Esta experiencia educativa de se ubica en el Área de Formación Terminal, ofrece un valor de 6 créditos.', 6, 6);
INSERT INTO materia VALUES(19, 2, 5, 'Apreciación del cine', 'Eleccion libre', 9, 4);
INSERT INTO materia VALUES(20, 2, 5, 'Introducción al teatro', 'Eleccion libre', 9, 4);
INSERT INTO materia VALUES(21, 3, 1, 'Lectura y escritura de textos', 'El propósito principal del curso-taller es contribuir al desarrollo de las competencias.', 4, 1);
INSERT INTO materia VALUES(22, 3, 1, 'Lengua I', 'La EE se trabaja en diferentes ambientes de aprendizaje en donde las 90 horas se distribuyen entre el trabajo presencial y autónomo', 4, 1);
INSERT INTO materia VALUES(23, 3, 2, 'Introducción al pensamiento computacional', 'El estudiante resuelve problemas, mediante la implementación de algoritmos computacionales.', 9, 2);
INSERT INTO materia VALUES(24, 3, 2, 'Algoritmos y programación', 'El estudiante implementa soluciones computacionales a problemas específicos.', 9, 2);
INSERT INTO materia VALUES(25, 3, 3, 'Networking', 'El estudiante configura a un nivel básico equipo de comunicaciones.', 9, 3);
INSERT INTO materia VALUES(26, 3, 3, 'Etica y gestión normativa', 'El estudiante analiza las normas y leyes para las licitaciones de software, hardware.', 6, 6);
INSERT INTO materia VALUES(27, 3, 4, 'Experiencia recepcional', 'El estudiante aplica los conocimientos y habilidades adquiridas a lo largo de la carrera', 12, 7);
INSERT INTO materia VALUES(28, 3, 4, 'Servicio Social', 'Esta experiencia educativa busca que el estudiante ponga en práctica conocimientos, habilidades y actitudes obtenidas.', 12, 8);
INSERT INTO materia VALUES(29, 3, 5, 'Francés I', 'Eleccion libre', 9, 4);
INSERT INTO materia VALUES(30, 3, 5, 'Fútbol', 'Eleccion libre', 9, 4);
INSERT INTO materia VALUES(31, 4, 1, 'Pensamiento crítico para la resolución de problemas', 'El estudiante comprende de manera crítica los conceptos de problema y solución', 4, 1);
INSERT INTO materia VALUES(32, 4, 1, 'Lengua I', 'Los estudiantes se comunican en inglés de manera oral y escrita en un nivel básico', 4, 1);
INSERT INTO materia VALUES(33, 4, 2, 'Calculo aplicado a la estadística I', 'El estudiante utiliza la teoría cálculo diferencial e integral.', 9, 2);
INSERT INTO materia VALUES(34, 4, 2, 'Pensamiento y cultura estadística', 'El estudiante desarrolla la comprensión de los principios y técnicas elementales de la estadística.', 8, 2);
INSERT INTO materia VALUES(35, 4, 3, 'Manejadores de bases de datos', 'El estudiante consulta bases de datos tanto relacionales como no relacionales mediante el empleo de fundamentos.', 8, 3);
INSERT INTO materia VALUES(36, 4, 3, 'Big Data', 'El estudiante es competente para, a partir del planteamiento de un programa de análisis de datos.', 8, 3);
INSERT INTO materia VALUES(37, 4, 4, 'Servicio Social', 'Esta experiencia educativa busca que el estudiante ponga en práctica conocimientos, habilidades y actitudes obtenidas.', 12, 6);
INSERT INTO materia VALUES(38, 4, 4, 'Acreditación del idioma inglés', 'Esta experiencia educativa de se ubica en el Área de Formación Terminal, ofrece un valor de 6 créditos.', 6, 7);
INSERT INTO materia VALUES(39, 4, 5, 'Fotografía', 'Eleccion libre', 9, 4);
INSERT INTO materia VALUES(40, 4, 5, 'Japonés I', 'Eleccion libre', 9, 4);
INSERT INTO materia VALUES(41, 5, 1, 'Computacion básica', 'El estudiante realiza prácticas individuales y grupales empleando herramientas digitales.', 6, 1);
INSERT INTO materia VALUES(42, 5, 1, 'Introducción a la programación', 'Introducción a la programación en la carrera de Tecnologías Computacionales.', 8, 1);
INSERT INTO materia VALUES(43, 5, 2, 'Álgebra lineal para computación', 'Álgebra lineal para computación en la carrera de Tecnologías Computacionales', 8, 2);
INSERT INTO materia VALUES(44, 5, 2, 'Programación', 'Programación en la carrera de Tecnologías Computacionales, se localiza en el área de formación disciplinaria', 8, 2);
INSERT INTO materia VALUES(45, 5, 3, 'Matemáticas discretas', 'Matemáticas discretas en la carrera de Tecnologías Computacionales, se localiza en el área de formación disciplinaria', 8, 3);
INSERT INTO materia VALUES(46, 5, 3, 'Estructuras de datos', 'Estructuras de datos en la carrera de Tecnologías Computacionales, se localiza en el área de formación disciplinaria', 9, 3);
INSERT INTO materia VALUES(47, 5, 4, 'Acreditación del idioma inglés', 'Esta experiencia educativa de se ubica en el Área de Formación Terminal, ofrece un valor de 6 créditos.', 6, 5);
INSERT INTO materia VALUES(48, 5, 4, 'Servicio social', 'Esta práctica profesional se encuentra ubicada en el área terminal del plan de estudios.', 12, 8);
INSERT INTO materia VALUES(49, 5, 5, 'Voleibol', 'Eleccion libre', 9, 4);
INSERT INTO materia VALUES(50, 5, 5, 'ITS', 'Eleccion libre', 9, 4);
INSERT INTO grado_estudios VALUES(1, 'Licenciatura');
INSERT INTO grado_estudios VALUES(2, 'Maestría');
INSERT INTO grado_estudios VALUES(3, 'Doctorado');
INSERT INTO profesor VALUES(1, 3, 'Carlos', 'Valdez', 'Solano', 'cvalsol@gmail.com');
INSERT INTO profesor VALUES(2, 2, 'Teresa', 'Rosas', 'Hernández', 'ter21rohergmail.com');
INSERT INTO profesor VALUES(3, 2, 'Roberto', 'Gutiérrez', 'Rios', 'rrios09@gmail.com');
INSERT INTO profesor VALUES(4, 1, 'Amanda', 'Castillo', 'Flores', 'amacast34@gmail.com');
INSERT INTO profesor VALUES(5, 3, 'Lorena', 'Méndez', 'Garcia', 'lormendez42@gmail.com');
INSERT INTO profesor VALUES(6, 3, 'Victor', 'Moreno', 'Miranda', 'victormormir29@gmai.com');
INSERT INTO profesor VALUES(7, 2, 'Karina', 'Lezama', 'Quintana', 'karlez12@gmail.com');
INSERT INTO profesor VALUES(8, 1, 'Gloria', 'Vargas', 'Méndez', 'glomen11@gmail.com');
INSERT INTO profesor VALUES(9, 3, 'Gerardo', 'Vázquez', 'Espinoza', 'gerva07@gmail.com');
INSERT INTO profesor VALUES(10, 2, 'Rosa', 'Perez', 'Hernández', 'perezros39@gmail.com'); 
INSERT INTO oferta VALUES(12345, 1, 4, 1);
INSERT INTO oferta VALUES(28902, 2, 3, 6);
INSERT INTO oferta VALUES(43658, 3, 2, 3);
INSERT INTO oferta VALUES(91637, 4, 1, 7);
INSERT INTO oferta VALUES(85721, 5, 1, 5);
INSERT INTO oferta VALUES(63028, 6, 3, 10);
INSERT INTO oferta VALUES(73082, 7, 4, 1);
INSERT INTO oferta VALUES(66273, 8, 4, 8);
INSERT INTO oferta VALUES(18234, 9, 4, 7);
INSERT INTO oferta VALUES(72736, 10, 4, 6);
INSERT INTO oferta VALUES(01922, 11, 1, 5);
INSERT INTO oferta VALUES(28392, 12, 1, 2);
INSERT INTO oferta VALUES(94723, 13, 2, 4);
INSERT INTO oferta VALUES(36482, 14, 2, 3);
INSERT INTO oferta VALUES(62849, 15, 3, 1);
INSERT INTO oferta VALUES(72364, 16, 3, 10);
INSERT INTO oferta VALUES(17394, 17, 2, 9);
INSERT INTO oferta VALUES(94384, 18, 4, 6);
INSERT INTO oferta VALUES(28463, 19, 1, 5);
INSERT INTO oferta VALUES(24830, 20, 4, 3);
INSERT INTO oferta VALUES(19347, 21, 1, 2);
INSERT INTO oferta VALUES(28374, 22, 1, 2);
INSERT INTO oferta VALUES(84738, 23, 2, 3);
INSERT INTO oferta VALUES(27374, 24, 2, 9);
INSERT INTO oferta VALUES(37483, 25, 3, 10);
INSERT INTO oferta VALUES(53748, 26, 1, 2);
INSERT INTO oferta VALUES(23774, 27, 1, 3);
INSERT INTO oferta VALUES(52737, 28, 1, 8);
INSERT INTO oferta VALUES(64839, 29, 1, 7);
INSERT INTO oferta VALUES(74638, 30, 4, 6);
INSERT INTO carga_academica VALUES('S19030017', 12345, 9.5);
INSERT INTO carga_academica VALUES('S23043019', 28902, 8.0);
INSERT INTO carga_academica VALUES('S20123456', 43658, 10.0);
INSERT INTO carga_academica VALUES('S21016023', 91637, 5.0);
INSERT INTO carga_academica VALUES('S20030096', 63028, 10.0);
INSERT INTO carga_academica VALUES('S22098096', 94384, 10.0);
INSERT INTO carga_academica VALUES('S22085094', 64839, 5.0);
INSERT INTO carga_academica VALUES('S20938474', 74638, 10.0);
