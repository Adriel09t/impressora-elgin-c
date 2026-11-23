# 🖨️ Impressora Elgin em C

Programa em **linguagem C** que controla uma impressora térmica **Elgin i8 / i9** pelo terminal do Windows, usando a biblioteca oficial da Elgin (`E1_Impressora01.dll`).

---

## 📘 O que o programa faz

Ao abrir, o programa pede **login** (3 tentativas) e mostra um **menu** que se repete até o usuário escolher sair. Pelo menu é possível:

- configurar, abrir e fechar a conexão com a impressora;
- imprimir texto (com várias cópias), QR Code e código de barras;
- imprimir o cupom fiscal **XML SAT** e o **XML de cancelamento SAT**;
- abrir a gaveta de dinheiro (dois comandos diferentes);
- emitir sinal sonoro (apito).

Nenhuma pergunta de impressão é feita se a conexão estiver fechada, e o retorno de cada comando da impressora é conferido, com mensagem de sucesso ou de erro.

---

## 🔐 Login de teste

| Usuário | Senha |
|---------|-------|
| `admin` | `1234` |

---

## 📋 Opções do menu

| Nº | Opção |
|----|-------|
| 1 | Configurar conexão |
| 2 | Abrir conexão |
| 3 | Fechar conexão |
| 4 | Imprimir texto |
| 5 | Imprimir QR Code |
| 6 | Imprimir código de barras |
| 7 | Imprimir XML SAT |
| 8 | Imprimir XML de cancelamento SAT |
| 9 | Abrir gaveta (Elgin) |
| 10 | Abrir gaveta |
| 11 | Sinal sonoro |
| 0 | Sair |

Valores para teste na opção 1: tipo `1` (USB), modelo `i9` (ou `i8`), conexão `USB`, parâmetro `0`.

---

## 📁 Arquivos do projeto

```
main.c                  → código do programa (único arquivo editado)
E1_Impressora01.dll     → biblioteca da Elgin (versão x64 / 64 bits)
XMLSAT.xml              → XML de teste do cupom
CANC_SAT.xml            → XML de teste do cancelamento
README.md               → este arquivo
```

Os quatro primeiros arquivos precisam ficar **na mesma pasta**, a raiz do projeto.

---

## ⚙️ Como compilar e executar

### 1. Qual DLL usar (32 ou 64 bits)

A DLL precisa ter a mesma arquitetura do compilador. Para descobrir o do seu, rode no terminal:

```
gcc -dumpmachine
```

| Resultado | Compilador | DLL |
|-----------|-----------|-----|
| `x86_64-w64-mingw32` | 64 bits | **x64** |
| `mingw32` ou `i686-w64-mingw32` | 32 bits | **x86** |

Este projeto foi feito com a DLL **x64 (64 bits)**.

### 2. Compilar e rodar

Ligue a impressora, conecte o cabo USB e, no terminal, dentro da pasta do projeto:

```
gcc main.c -o impressora.exe
impressora.exe
```

### Code::Blocks

Crie um projeto *Console application → C*, troque o conteúdo do `main.c` pelo deste repositório, copie a DLL e os XMLs para a pasta do projeto e confira em *Project → Properties → Build targets* se o **Execution working dir** é a pasta do projeto.

---

## 🛠️ Se der erro

| Mensagem | Causa provável |
|----------|----------------|
| `erro 126` ao carregar a DLL | DLL fora da pasta de onde o programa roda |
| `erro 193` ao carregar a DLL | DLL com bits diferentes do compilador |
| `Comando '...' nao encontrado na DLL` | DLL errada ou de outra versão |
| `Erro ao abrir conexao` (código negativo) | Impressora desligada, cabo solto ou dados da opção 1 errados |
| `Nao foi possivel ler o XML` | XMLs fora da pasta de execução |

---

## 👥 Integrantes

- Adriel Ebler Corradi Tavares Pereira
- Klecio Ferreira Santos
