# Verificador de Código C com ESBMC no Google Colab

Este projeto demonstra o funcionamento do **[ESBMC](https://esbmc.org/)** (Efficient SMT-Based Bounded Model Checker) de forma automatizada no **Google Colab**.  
O script localiza um arquivo `.c`, renomeia para `main.c`, executa a verificação no ESBMC e salva as **claims** encontradas em formato `.txt` e `.csv`.

---

## Como usar no Google Colab

### 1. Abrir o notebook no Colab
- Acesse o Google Colab.
- Importe ou copie o conteúdo do script `verificador_c_esbmc_colab.py` para uma célula.
- Certifique-se de que o runtime é **Python 3**.

---

### 2. Preparar um arquivo C para teste
O script procura um arquivo `.c` na raiz (`/content`) e o renomeia para `main.c`.

**Opção A — Fazer upload do seu código**
- Clique no ícone de **pasta** no Colab.
- Clique em **Upload** e envie seu arquivo `.c`.

**Opção B — Criar um exemplo de teste no Colab**
```bash
%%bash
cat > /content/exemplo.c <<'EOF'
#undef NDEBUG
#include <assert.h>

int soma_ate_n(int n) {
  int s = 0;
  for (int i = 0; i < n; i++) s += i;
  return s;
}

int main() {
  int s = soma_ate_n(5); // 0+1+2+3+4 = 10
  assert(s == 20);       // <- violação proposital
  return 0;
}
EOF

---

### 3. Executar o script
O script irá:

1. Limpar arquivos e pastas antigos.

2. Localizar o primeiro .c e renomear para main.c.

3. Baixar e extrair a versão pré-compilada do ESBMC.

4. Conceder permissão de execução ao binário.

5. Executar a verificação no main.c.

6. Listar e salvar as claims:

**saida.txt (texto puro)**

**dados.csv (tabela com Claim, Linha e Expressão)**
