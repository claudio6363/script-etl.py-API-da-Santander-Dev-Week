import json
import pandas as pd

# -------------------------------
# 1. EXTRAÇÃO
# -------------------------------
usuarios = [
    {"id": 1, "nome": "Ana", "idade": 28, "cidade": "São Paulo"},
    {"id": 2, "nome": "Carlos", "idade": 35, "cidade": "Rio de Janeiro"},
    {"id": 3, "nome": "Mariana", "idade": 22, "cidade": "Belo Horizonte"},
    {"id": 4, "nome": "João", "idade": 40, "cidade": "Curitiba"},
    {"id": 5, "nome": "Fernanda", "idade": 19, "cidade": "Recife"}
]

# -------------------------------
# 2. TRANSFORMAÇÃO
# -------------------------------
for usuario in usuarios:
    # Normalizar nome
    usuario["nome"] = usuario["nome"].upper()
    
    # Criar faixa etária
    if usuario["idade"] < 25:
        usuario["faixa_etaria"] = "Jovem"
    elif usuario["idade"] < 40:
        usuario["faixa_etaria"] = "Adulto"
    else:
        usuario["faixa_etaria"] = "Experiente"
    
    # Mensagem personalizada
    usuario["mensagem"] = f"Olá {usuario['nome']}, temos novidades para você em {usuario['cidade']}!"

# -------------------------------
# 3. CARREGAMENTO
# -------------------------------
# Salvar em JSON
with open("usuarios.json", "w", encoding="utf-8") as f:
    json.dump(usuarios, f, ensure_ascii=False, indent=4)

# Salvar em CSV usando pandas
df = pd.DataFrame(usuarios)
df.to_csv("usuarios.csv", index=False, encoding="utf-8")

# -------------------------------
# 4. ESTATÍSTICAS SIMPLES
# -------------------------------
print("📊 Estatísticas dos Usuários")
print("Média de idade:", df["idade"].mean())
print("Distribuição por cidade:")
print(df["cidade"].value_counts())
print("Distribuição por faixa etária:")
print(df["faixa_etaria"].value_counts())
