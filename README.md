CREATE DATABASE envios;
USE envios;


CREATE TABLE envios (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    pedido_id BIGINT NOT NULL,
    cliente_id BIGINT NOT NULL,
    estado VARCHAR(30) NOT NULL,
    numero_tracking VARCHAR(100),
    fecha_creacion DATETIME NOT NULL,
    fecha_entrega_estimada DATETIME,
    fecha_entrega_real DATETIME
);


CREATE TABLE direcciones_envio (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    envio_id BIGINT NOT NULL,
    calle VARCHAR(100),
    ciudad VARCHAR(50),
    codigo_postal VARCHAR(20),
    pais VARCHAR(50),
    telefono VARCHAR(30),
    nombre_contacto VARCHAR(100),
    FOREIGN KEY (envio_id) REFERENCES envios(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);


CREATE TABLE tracking_eventos (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    envio_id BIGINT NOT NULL,
    descripcion VARCHAR(255),
    ubicacion VARCHAR(100),
    fecha_evento DATETIME,
    FOREIGN KEY (envio_id) REFERENCES envios(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

INSERT INTO envios (pedido_id, cliente_id, estado, numero_tracking, fecha_creacion, fecha_entrega_estimada, fecha_entrega_real)
VALUES
  (1, 1001, 'EN_PREPARACION', 'TRACK-ABCD1234', '2025-06-11 10:00:00', '2025-06-13 18:00:00', NULL),
  (2, 1002, 'EN_TRANSITO', 'TRACK-EFGH5678', '2025-06-11 12:30:00', '2025-06-14 20:00:00', NULL);
  
  INSERT INTO direcciones_envio (envio_id, calle, ciudad, codigo_postal, pais, telefono, nombre_contacto)
VALUES
  (1, 'Av. Central 123', 'Santiago', '8320000', 'Chile', '+56912345678', 'Lucas Arevalo'),
  (2, 'Calle Sur 456', 'Valparaíso', '2340000', 'Chile', '+56987654321', 'María López');

INSERT INTO tracking_eventos (envio_id, descripcion, ubicacion, fecha_evento)
VALUES
  (1, 'Envío creado', 'Centro de distribución', '2025-06-11 10:05:00'),
  (1, 'En camino al cliente', 'Ruta 68', '2025-06-12 08:30:00'),
  (2, 'Envío creado', 'Centro de distribución', '2025-06-11 12:35:00'),
  (2, 'En tránsito', 'Terminal Valparaíso', '2025-06-13 09:45:00');
