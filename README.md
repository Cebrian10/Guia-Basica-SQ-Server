# Comandos útiles en SQL

## 1. Creación de una Base de Datos

### Primera forma

```
Create Database NOMBRE_DE_BD
```

### Segunda forma
```
Create Database NOMBRE_DE_BD on Primary(
    Name = NOMBRE_DE_BD,
	Filename = 'C:\NOMBRE_DE_BD.mdf',
	Size = 50 MB,
	Maxsize = Unlimited,
	Filegrowth = 50 MB
)
log on(
	Name = NOMBRE_DE_BD_log,
	Filename = 'C:\NOMBRE_DE_BD_log.ldf',
	Size = 50 MB,
	Maxsize = Unlimited,
	Filegrowth = 50 MB
)
```

## 2. Creación de Tablas
```
Create Table NOMBRE_TABLA(
	NOMBRE_COLUMNA TIPO_DE_DATO(TAMAÑO) NOT NULL
	Constraint NOMBRE_TABLA_ATRIBUTO_pk PRIMARY KEY
)
```

## 3. Restricciones

Se recomienda el formato tabla_atributo_tipoRestriccion.

Tipos de restricciones:
- Primary Key [ pk ]
- Foreign Key [ fk ]
- Check [ ck ]
- Default [ df ]
- Unique [ uq ]

## 4. Alter

### Añadir una llave primaria
```
Alter Table NOMBRE_TABLA
Add Constraint NOMBRE_TABLA_ATRIBUTO_pk PRIMARY KEY
```


### Añadir una llave foránea
```
Alter Table NOMBRE_TABLA
Add Constraint NOMBRE_TABLA_ATRIBUTO_fk
FOREIGN KEY ([columna_hija]) REFERENCES [tabla_padre] ([columna_padre])
```


### Cambiar un tipo de dato
```
Alter Table NOMBRE_TABLA
Alter Column NOMBRE_COLUMNA tipoDato
```


### Eliminar una columna
```
Alter Table NOMBRE_TABLA
Drop Column NOMBRE_TABLA
```


### Agregar una columna
```
Alter Table NOMBRE_TABLA
Add NOMBRE_COLUMNA tipoDato
```


## 5. Drop

### Eliminar una Base de Datos
```
Drop Database NOMBRE_BD
```


### Eliminar Restricción
```
Alter Table NOMBRE_TABLA
Drop Constraint NOMBRE_TABLA_ATRIBUTO_pk
```


### Eliminar una tabla
```
Drop Table NOMBRE_TABLA
```


## 6. Ayuda

### Comandos para saber qué restricciones tiene una tabla
```
Sp_Help NOMBRE_TABLA
Sp_HelpConstraint NOMBRE_TABLA
```


## 7. Insert

### Insert en una tupla
```
Insert into NOMBRE_TABLA(columna1, columna2)
values('nombre', edad)
```


### Insertar como resultado de un select
```
Insert into NOMBRE_TABLA(columna1)
Select Distinct columna1
From OTRA_TABLA
```


## 8. Delete

### Eliminar toda una tupla
```
Delete NOMBRE_TABLA
```


### Eliminar una tupla específica
```
Delete NOMBRE_TABLA
Where NOMBRE_COLUMNA = 7
```


### Eliminar como resultado de un select
```
Delete From NOMBRE_TABLA
Where NOMBRE_COLUMNA in(
    Select NOMBRE_COLUMNA
    From OTRA_TABLA
    Where NOMBRE_COLUMNA = 'Dorado'
)
```


## 9. Update

### Modificando el registro 106
```
Update NOMBRE_TABLA
Set NOMBRE_COLUMNA = 'sistemas'
Where NOMBRE_COLUMNA = 106
```


### Actualizar con CASE
```
Update NOMBRE_TABLA
Set NOMBRE_COLUMNA = (
CASE NOMBRE_COLUMNA
    when 'literatura' then 1
    when 'matematicas' then 2
    when 'sistemas' then 3
    Else 0
END
)
```


## 10. Check

### Crear una tabla con diferentes Checks
```
Create Table NOMBRE_TABLA(
    atributo1 int NOT NULL
    Constraint NOMBRE_TABLA_ATRIBUTO1_pk PRIMARY KEY,
    atributo2 nchar(8)
    Constraint NOMBRE_TABLA_ATRIBUTO2_ck
        CHECK(atributo2 in ('uno','dos','tres')),
    atributo3 nchar(9)
    Constraint NOMBRE_TABLA_ATRIBUTO3_ck
        CHECK(atributo3 in ('lunes','miercoles','viernes'))
    Constraint NOMBRE_TABLA_ATRIBUTO3_df
        DEFAULT('lunes'),
    atributo4 nchar(13)
    Constraint NOMBRE_TABLA_ATRIBUTO4_ck
        CHECK(atributo4 LIKE '[0][0-9][-][0-9][0-9][A-Z][0-9]'),
    atributo5 money
    Constraint NOMBRE_TABLA_ATRIBUTO5_ck
        CHECK(atributo5 > 0)
)
```
