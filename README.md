# curso-postgresql


primeiro comando:


```shell
$ psql -U usuario -d banco_de_dados -c "SELECT version();"

```


```sql
-- Exemplo de código PostgreSQL com syntax highlighting
CREATE TABLE estudantes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE,
    matriculado BOOLEAN DEFAULT FALSE
);

-- Função PL/pgSQL
CREATE OR REPLACE FUNCTION total_estudantes() 
RETURNS INTEGER AS $$
DECLARE
    total INTEGER;
BEGIN
    SELECT COUNT(*) INTO total FROM estudantes;
    RETURN total;
END;
$$ LANGUAGE plpgsql;
```



# Links de Apoio
- [PSQL on line](https://pg-sql.com/)
