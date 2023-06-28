-- phpMyAdmin SQL Dump
-- version 5.2.1
-- https://www.phpmyadmin.net/
--
-- Servidor: 127.0.0.1
-- Tiempo de generación: 21-06-2023 a las 18:40:50
-- Versión del servidor: 10.4.28-MariaDB
-- Versión de PHP: 8.0.28

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Base de datos: `veterinaria4`
--

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `cita`
--

CREATE TABLE `cita` (
  `ID_CITA` int(11) NOT NULL,
  `FECHA` datetime DEFAULT NULL,
  `ID_DOCTOR` varchar(45) DEFAULT NULL,
  `ID_MASCOTA` int(11) NOT NULL,
  `ID_CLIENTE` int(11) NOT NULL,
  `ID_SERVICIO` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

--
-- Volcado de datos para la tabla `cita`
--

INSERT INTO `cita` (`ID_CITA`, `FECHA`, `ID_DOCTOR`, `ID_MASCOTA`, `ID_CLIENTE`, `ID_SERVICIO`) VALUES
(1, '2016-11-23 09:20:00', '0', 2, 1, 3);

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `cliente`
--

CREATE TABLE `cliente` (
  `ID_CLIENTE` int(11) NOT NULL,
  `PERSONA_CI` char(8) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

--
-- Volcado de datos para la tabla `cliente`
--

INSERT INTO `cliente` (`ID_CLIENTE`, `PERSONA_CI`) VALUES
(1, '76935184'),
(2, '76935185');

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `historia_clinica`
--

CREATE TABLE `historia_clinica` (
  `NUMERO_HC` int(11) NOT NULL,
  `MASCOTA_ID_MASCOTA` int(11) NOT NULL,
  `NUTRICION` varchar(50) DEFAULT NULL,
  `ESTILO_VIDA` varchar(200) DEFAULT NULL,
  `TEMPERATURA` decimal(10,0) DEFAULT NULL,
  `PULSO` int(11) DEFAULT NULL,
  `ESTADO_HIDRATACION` varchar(45) DEFAULT NULL,
  `FRECUENCIA_CARDIACA` decimal(10,0) DEFAULT NULL,
  `FRECUENCIA_RESPIRATORIA` decimal(10,0) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

--
-- Volcado de datos para la tabla `historia_clinica`
--

INSERT INTO `historia_clinica` (`NUMERO_HC`, `MASCOTA_ID_MASCOTA`, `NUTRICION`, `ESTILO_VIDA`, `TEMPERATURA`, `PULSO`, `ESTADO_HIDRATACION`, `FRECUENCIA_CARDIACA`, `FRECUENCIA_RESPIRATORIA`) VALUES
(1, 1, 'Pedigree', 'en casa', 40, 80, '6', 80, 34),
(2, 2, NULL, NULL, 36, 40, '7', 12, 13),
(3, 3, NULL, NULL, 40, 60, '9', 90, 90);

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `mascota`
--

CREATE TABLE `mascota` (
  `ID_MASCOTA` int(11) NOT NULL,
  `NOMBRE` varchar(45) DEFAULT NULL,
  `COLOR` varchar(20) DEFAULT NULL,
  `ESPECIE` varchar(50) DEFAULT NULL,
  `RAZA` varchar(45) DEFAULT NULL,
  `PROPIETARIO_CI` char(8) DEFAULT NULL,
  `GENERO` char(1) DEFAULT NULL,
  `NUMERO_HC` int(11) DEFAULT NULL,
  `EDAD` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

--
-- Volcado de datos para la tabla `mascota`
--

INSERT INTO `mascota` (`ID_MASCOTA`, `NOMBRE`, `COLOR`, `ESPECIE`, `RAZA`, `PROPIETARIO_CI`, `GENERO`, `NUMERO_HC`, `EDAD`) VALUES
(1, 'Escot', 'gris', 'Canino', 'shitzu', '76935184', 'M', 0, 8),
(2, 'sessa', 'marron', 'Canino', 'shitzu', '76935184', 'H', NULL, 12),
(3, 'duke', 'negro', 'Canino', 'boxer', '76935185', 'M', NULL, 7);

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `persona`
--

CREATE TABLE `persona` (
  `PERSONA_CI` char(8) NOT NULL,
  `NOMBRES` varchar(50) DEFAULT NULL,
  `APELLIDOS` varchar(50) DEFAULT NULL,
  `GENERO` char(1) DEFAULT NULL,
  `EDAD` int(11) DEFAULT NULL,
  `TELEFONO` varchar(15) DEFAULT NULL,
  `DIRECCION` varchar(300) DEFAULT NULL,
  `CORREO` varchar(80) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

--
-- Volcado de datos para la tabla `persona`
--

INSERT INTO `persona` (`PERSONA_CI`, `NOMBRES`, `APELLIDOS`, `GENERO`, `EDAD`, `TELEFONO`, `DIRECCION`, `CORREO`) VALUES
('76935184', 'Carlos', 'Chavez Laguna', 'M', 28, '948110940', 'jr pataz 1344', 'carloscl94r@gmail.com'),
('76935185', 'Maria', 'Tello Cisneros', 'F', 23, '555555', 'donde sea', 'maria@hotmail.com');

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `servicio`
--

CREATE TABLE `servicio` (
  `ID_SERVICIO` int(11) NOT NULL,
  `ID_MASCOTA` int(11) NOT NULL,
  `ESTADO` varchar(15) DEFAULT NULL,
  `ID_CLIENTE` int(11) NOT NULL,
  `ID_TIPO_SERVICIO` int(11) DEFAULT NULL,
  `SUBTOTAL` decimal(10,0) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

--
-- Volcado de datos para la tabla `servicio`
--

INSERT INTO `servicio` (`ID_SERVICIO`, `ID_MASCOTA`, `ESTADO`, `ID_CLIENTE`, `ID_TIPO_SERVICIO`, `SUBTOTAL`) VALUES
(1, 2, 'PENDIENTE', 1, 3, 20),
(2, 1, 'PENDIENTE', 1, 10, 120),
(3, 2, 'PENDIENTE', 1, 3, 20),
(4, 3, 'PENDIENTE', 2, 3, 20);

-- --------------------------------------------------------

--
-- Estructura de tabla para la tabla `tipo_servicio`
--

CREATE TABLE `tipo_servicio` (
  `ID_TIPO_SERVICIO` int(11) NOT NULL,
  `NOMBRE` varchar(50) DEFAULT NULL,
  `PRECIO` decimal(10,0) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

--
-- Volcado de datos para la tabla `tipo_servicio`
--

INSERT INTO `tipo_servicio` (`ID_TIPO_SERVICIO`, `NOMBRE`, `PRECIO`) VALUES
(3, 'Consulta', 20),
(4, 'Vacunación', 40),
(5, 'Hematologia', 40),
(6, 'Sedimiento urinario', 50),
(7, 'Cultivo y antibiograma', 60),
(8, 'Parvovirosis canina', 50),
(9, 'Panleucopenia felina', 40),
(10, 'Hospitalización', 30);

--
-- Índices para tablas volcadas
--

--
-- Indices de la tabla `cita`
--
ALTER TABLE `cita`
  ADD PRIMARY KEY (`ID_CITA`,`ID_MASCOTA`,`ID_CLIENTE`),
  ADD KEY `fk_CITA_MASCOTA1_idx` (`ID_MASCOTA`),
  ADD KEY `fk_CITA_CLIENTE1_idx` (`ID_CLIENTE`),
  ADD KEY `FK_CITA_SERVICIO` (`ID_SERVICIO`);

--
-- Indices de la tabla `cliente`
--
ALTER TABLE `cliente`
  ADD PRIMARY KEY (`ID_CLIENTE`,`PERSONA_CI`),
  ADD KEY `fk_CLIENTE_PERSONA_idx` (`PERSONA_CI`);

--
-- Indices de la tabla `historia_clinica`
--
ALTER TABLE `historia_clinica`
  ADD PRIMARY KEY (`NUMERO_HC`,`MASCOTA_ID_MASCOTA`),
  ADD KEY `fk_HISTORIA_CLINICA_MASCOTA1_idx` (`MASCOTA_ID_MASCOTA`);

--
-- Indices de la tabla `mascota`
--
ALTER TABLE `mascota`
  ADD PRIMARY KEY (`ID_MASCOTA`);

--
-- Indices de la tabla `persona`
--
ALTER TABLE `persona`
  ADD PRIMARY KEY (`PERSONA_CI`);

--
-- Indices de la tabla `servicio`
--
ALTER TABLE `servicio`
  ADD PRIMARY KEY (`ID_SERVICIO`,`ID_MASCOTA`,`ID_CLIENTE`),
  ADD KEY `fk_SERVICIO_MASCOTA1_idx` (`ID_MASCOTA`),
  ADD KEY `fk_SERVICIO_CLIENTE1_idx` (`ID_CLIENTE`),
  ADD KEY `FK_TIPO_SERVICIO_SERVICIO` (`ID_TIPO_SERVICIO`);

--
-- Indices de la tabla `tipo_servicio`
--
ALTER TABLE `tipo_servicio`
  ADD PRIMARY KEY (`ID_TIPO_SERVICIO`);

--
-- AUTO_INCREMENT de las tablas volcadas
--

--
-- AUTO_INCREMENT de la tabla `cita`
--
ALTER TABLE `cita`
  MODIFY `ID_CITA` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=2;

--
-- AUTO_INCREMENT de la tabla `cliente`
--
ALTER TABLE `cliente`
  MODIFY `ID_CLIENTE` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=3;

--
-- AUTO_INCREMENT de la tabla `historia_clinica`
--
ALTER TABLE `historia_clinica`
  MODIFY `NUMERO_HC` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=4;

--
-- AUTO_INCREMENT de la tabla `mascota`
--
ALTER TABLE `mascota`
  MODIFY `ID_MASCOTA` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=4;

--
-- AUTO_INCREMENT de la tabla `servicio`
--
ALTER TABLE `servicio`
  MODIFY `ID_SERVICIO` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=5;

--
-- AUTO_INCREMENT de la tabla `tipo_servicio`
--
ALTER TABLE `tipo_servicio`
  MODIFY `ID_TIPO_SERVICIO` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=11;

--
-- Restricciones para tablas volcadas
--

--
-- Filtros para la tabla `cita`
--
ALTER TABLE `cita`
  ADD CONSTRAINT `FK_CITA_SERVICIO` FOREIGN KEY (`ID_SERVICIO`) REFERENCES `servicio` (`ID_SERVICIO`),
  ADD CONSTRAINT `fk_CITA_CLIENTE1` FOREIGN KEY (`ID_CLIENTE`) REFERENCES `cliente` (`ID_CLIENTE`) ON DELETE NO ACTION ON UPDATE NO ACTION,
  ADD CONSTRAINT `fk_CITA_MASCOTA1` FOREIGN KEY (`ID_MASCOTA`) REFERENCES `mascota` (`ID_MASCOTA`) ON DELETE NO ACTION ON UPDATE NO ACTION;

--
-- Filtros para la tabla `cliente`
--
ALTER TABLE `cliente`
  ADD CONSTRAINT `fk_CLIENTE_PERSONA` FOREIGN KEY (`PERSONA_CI`) REFERENCES `persona` (`PERSONA_CI`) ON DELETE NO ACTION ON UPDATE NO ACTION;

--
-- Filtros para la tabla `historia_clinica`
--
ALTER TABLE `historia_clinica`
  ADD CONSTRAINT `fk_HISTORIA_CLINICA_MASCOTA1` FOREIGN KEY (`MASCOTA_ID_MASCOTA`) REFERENCES `mascota` (`ID_MASCOTA`) ON DELETE NO ACTION ON UPDATE NO ACTION;

--
-- Filtros para la tabla `servicio`
--
ALTER TABLE `servicio`
  ADD CONSTRAINT `FK_TIPO_SERVICIO_SERVICIO` FOREIGN KEY (`ID_TIPO_SERVICIO`) REFERENCES `tipo_servicio` (`ID_TIPO_SERVICIO`),
  ADD CONSTRAINT `fk_SERVICIO_CLIENTE1` FOREIGN KEY (`ID_CLIENTE`) REFERENCES `cliente` (`ID_CLIENTE`) ON DELETE NO ACTION ON UPDATE NO ACTION,
  ADD CONSTRAINT `fk_SERVICIO_MASCOTA1` FOREIGN KEY (`ID_MASCOTA`) REFERENCES `mascota` (`ID_MASCOTA`) ON DELETE NO ACTION ON UPDATE NO ACTION;
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
