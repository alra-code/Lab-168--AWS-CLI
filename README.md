<div align="center">

# 💻 Lab 168 — Instale e Configure a AWS CLI

![AWS CLI](https://img.shields.io/badge/AWS-CLI-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Linux](https://img.shields.io/badge/Red_Hat-Linux-EE0000?style=for-the-badge&logo=redhat&logoColor=white)
![IAM](https://img.shields.io/badge/AWS-IAM-2E86C1?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-2ECC71?style=for-the-badge)

</div>

---

## 📌 Sobre o laboratório

A **AWS Command Line Interface (AWS CLI)** é uma ferramenta de linha de comando que fornece uma interface para interagir com produtos e serviços da AWS.

> 💡 **Cenário:** instalar e configurar a AWS CLI em uma instância **Red Hat Linux** (que não vem com a CLI pré-instalada), conectar-se via **SSH**, configurar uma chave de acesso e usar a CLI para interagir com o **AWS IAM**.

---

## 🎯 Objetivos

Ao concluir este laboratório, fui capaz de:

- ⚙️ Instalar e configurar a **AWS CLI**
- 🔗 Conectar a AWS CLI a uma **conta da AWS**
- 🔐 Acessar o **IAM** usando a AWS CLI

---

## 🗺️ Fluxo do laboratório

```
   🌍 Local/Browser                    ☁️ AWS Cloud
        │                                     │
        │   1️⃣ SSH                             │
        ├────────────────────► 🖥️ EC2 (Red Hat Linux)
        │                                     │
        │                         2️⃣ curl + unzip + install
        │                        ⚙️  AWS CLI instalada
        │                                     │
        │                         3️⃣ aws configure
        │                        🔑 Access Key + Secret Key
        │                        🌎 Região: us-west-2
        │                                     │
        │                         4️⃣ aws iam list-users
        │                        👤 awsstudent
        └─────────────────────────────────────┘
                    5️⃣ Validação cruzada:
              Console IAM  🆚  AWS CLI
```
![infra do la](./imagem/infra%20do%20la168.png)
---

## 🛠️ Etapas realizadas

### ✅ Tarefa 1 — Conectar-se à instância do EC2 do Red Hat usando SSH

Conexão **SSH** estabelecida com sucesso na instância EC2 Red Hat Linux, autenticando com uma chave pública (`imported-openssh-key`) via usuário `ec2-user`.

```bash
Using username "ec2-user".
Authenticating with public key "imported-openssh-key"
```

### ✅ Tarefa 2 — Instalar a AWS CLI em uma instância do Linux do Red Hat

Download, extração e instalação da AWS CLI v2 diretamente na instância, já que o Red Hat Linux **não vem com a CLI pré-instalada**.

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip -u awscliv2.zip
sudo ./aws/install
aws --version
```

```
aws-cli/2.37.7 Python/3.14.6 Linux/4.14.355-287.750.amzn2.x86_64 exe/x86_64
```

### ✅ Tarefa 3 — Observar os detalhes de configuração do IAM no Console de Gerenciamento da AWS

Inspeção do usuário **`awsstudent`** diretamente no console IAM, verificando políticas anexadas e credenciais de segurança já existentes antes de configurar a CLI.

| Item | Detalhe |
|:---|:---|
| 👤 Usuário | `awsstudent` |
| 📜 Políticas | `lab_policy` (gerenciada pelo cliente) + `ReadOnlyAccess` (via grupo `QLReadOnly`) |
| 🔑 Acesso ao console | Desabilitado |

### ✅ Tarefa 4 — Configurar a AWS CLI para conectar-se à conta da AWS

Configuração da AWS CLI com as credenciais do usuário IAM, definindo região e formato de saída padrão.

```bash
aws configure
AWS Access Key ID: AKIATZFRDV56PXR3466Y
AWS Secret Access Key: ********************************
Default region name: us-west-2
Default output format: json
```

### ✅ Tarefa 5 — Observar os detalhes de configuração do IAM usando a AWS CLI

Execução do comando `aws iam list-users` para validar, via terminal, as mesmas informações visualizadas anteriormente no console — confirmando que a CLI estava corretamente conectada à conta.

```bash
aws iam list-users
```

```json
{
    "Users": [
        {
            "Path": "/",
            "UserName": "awsstudent",
            "UserId": "AIDATZFRDV56BCNZQRNRD",
            "Arn": "arn:aws:iam::260216958844:user/awsstudent",
            "CreateDate": "2026-09-30T20:21:28+00:00"
        }
    ]
}
```

---

## ✅ Resultado final

A saída do comando `aws iam list-users` reproduziu, via linha de comando, exatamente o mesmo usuário visto antes no console web — confirmando que a **AWS CLI estava corretamente instalada, configurada e conectada** à conta da AWS. 🎉

---

## 🧠 Principais aprendizados

- 🔹 Como conectar-se a uma instância EC2 remotamente via **SSH**
- 🔹 Instalação manual da **AWS CLI v2** em sistemas que não a possuem pré-instalada
- 🔹 Uso do comando `aws configure` para autenticar a CLI com **Access Key** e **Secret Key**
- 🔹 Diferença entre interagir com a AWS pelo **console web** e pela **linha de comando**
- 🔹 Como validar permissões e identidade usando `aws iam list-users`

---

## 🏷️ Tecnologias e Serviços

![AWS CLI](https://img.shields.io/badge/AWS-CLI-232F3E?style=flat-square&logo=amazon-aws&logoColor=FF9900)
![Amazon EC2](https://img.shields.io/badge/Amazon-EC2-232F3E?style=flat-square&logo=amazon-aws&logoColor=FF9900)
![AWS IAM](https://img.shields.io/badge/AWS-IAM-232F3E?style=flat-square&logo=amazon-aws&logoColor=FF9900)
![Red Hat Linux](https://img.shields.io/badge/Red_Hat-Linux-EE0000?style=flat-square&logo=redhat&logoColor=white)
![SSH](https://img.shields.io/badge/Protocol-SSH-4EAA25?style=flat-square&logo=gnu-bash&logoColor=white)

---

<div align="center">

📚 *Laboratório prático realizado como parte da trilha de estudos em Computação em Nuvem, com foco em transição de carreira para Engenharia de Dados.*

</div>
