# Como trabalhar com Git offline
Esse material faz parte dos meus estudos em tecnologia e desenvolvimento. 
Para alguns pode ser algo simples, mas para outros possa ser que seja útil.

Bom o Git é um sistema de versionamento de código. Com ele você pode criar várias versões do seu código que funcionam como backups.
Isso permite que você pare de ficar duplicando o mesmo arquivo de código para fazer backup e utilize apenas o Git para que ele controle todas as suas features, testes, etc.

### Para começar você pode instalar o Git (que é diferente do Github) no seu computador.

Vá no google ou no seu buscador do browser e pesquise por Git Download. 

[https://git-scm.com/install/](https://git-scm.com/install/)

Site do Git, escolha seu sistema operacional, baixe e instale conforme as instruções.


#### Vamos precisar de alguns comandos no terminal

como:
```
cd (para entrar em alguma pasta)
cd .. (para voltar pastas)
```

---
Com o git instalado você pode verificar a versão digitando no terminal com o comando:

```bash
git --version
```

## 1. Setup inicial (uma vez por projeto)
Precisamos configurar a sua identidade no git para os **commits (mensagens das versões)**.

Crie uma pasta e abra ela no terminal.
Depois siga os seguintes comandos para inciar o git no seu projeto.
```bash
git init (inicia o arquivo do git no seu repositório)
git config --local user.name "seuusuario" (pode ser o mesmo username do github)
git config --local user.email "seuemail@email.com" (pode ser o mesmo e-mail que você loga no github)
```

o --local fica só no seu repositório ou pasta, se quiser que fique globalmente em qualquer pasta que você iniciar o git com **git init** pode configurar com --global no lugar do --local.

Verificar alterações:

```bash
git status
```

---

## 2. `.gitignore` (obrigatório)

O arquivo .gitignore caso não exista, você pode criar um, ele serve para bloquear que certos arquivos e pastas (diretórios), sejam vercionados ou enviados para o github, pois eles podem ser grandes ou conter algum conteúdo sensível.

Exemplo genérico de um .gitignore (ajuste conforme stack):

```
node_modules
.env
.env.*
dist
build
.next
out
coverage
.DS_Store
```

---

## 3. Primeiro commit
Crie um arquivo no seu repositório, pode ser um index.html escreva algo no arquivo e salve.

Em seguida você pode verificar com o comando git status, tudo o que foi alterado no seu repositório (pasta local)

```bash
git status (se tudo estiver ok você pode adicionar todos os arquivos modificados para o stage, um passo antes do commit (versionamento) do seu código)
git add . (adiciona todas as modifcações feitas para o stage)
git commit -m "init" (cria o seu commit ou mensagens para identificar aquela versão criada)
```

Dica: **nunca trabalhe sem commit inicial**. Pois você pode voltar ao projeto inicial caso alguma versão esteja ruim futuramente.

---

## 4. Conceito de branches

As branches são ramificações da branch main (que é a ramificação principal do seu código), com as branches você pode criar outra ramificação para fazer testes:
* `main` → versão estável
* `feature/*` → novas funcionalidades
* `fix/*` → correções
* `experiment/*` → testes descartáveis

Tudo **local**.

---

## 5. Fluxo padrão de trabalho (recomendado)

### Criar feature

```bash
git checkout -b feature-header
```

### Trabalhar + salvar progresso

crie seu arquivo index.html adicione um header e faça os seguintes comandos:

```bash
git status (verifica o que foi alterado)
git add . (o . adiciona todas as alterações, você pode digitar git add index.html só para adicionar ele)
git commit -m "feature: header inicial" (faz o commit/mensagem das suas alterações)
```

Faça commits **pequenos e frequentes** a cada modificação funcional, para salvar as versões do seu código.

---

## 6. Voltar para `main` e integrar a branch feature-header dentro da main

> O comando checkout serve para você mudar de branchs ou criar uma nova.

```bash
git chechout -a (lista todas as branchs disponíveis)
```

```bash
git checkout main (muda para a branch main)
git merge feature-header (faz a integração da branch feature-header com a main)
```

Se não quiser mais a branch:

```bash
git branch -d feature-header
```

---

## 7. Corrigir algo rápido (hotfix local)

```bash
git checkout -b fix-navbar
# corrige
git add .
git commit -m "fix: navbar overflow"
git checkout main
git merge fix-navbar
git branch -d fix-navbar
```

---

## 8. Ver histórico (use sempre)

```bash
git log --oneline --graph --all
```

Isso é seu **backup** ou controle de versão do seu código, vai mostrar alguns **hashs** e sua mensagem de commit

---

## 9. Voltar no tempo (sem medo)

### Só olhar um commit antigo

```bash
git checkout <hash>
```

Voltar para o presente:

```bash
git checkout main
```

### Resetar ou voltar para uma versão do projeto para um ponto específico (destrutivo)

```bash
git reset --hard <hash>
```

---

## 10. Experimentos seguros

Quer testar algo sem risco?

Crie uma nova branch:
```bash
git checkout -b experiment-ui
```

Se der ruim:

```bash
git checkout main
git branch -D experiment-ui
```

Zero impacto.

---

## 11. Tags (marcar versões locais)

```bash
git tag v1.0
git tag v1.1
```

Listar:

```bash
git tag
```

---

## 12. Boas práticas

* ❌ Nunca commit em `main` direto
* ✅ Crie uma branch por objetivo
* ✅ Commits pequenos
* ✅ Mensagem clara
* ❌ Nunca versionar `.env` e outros arquivos que você não quer que outras pessoas vejam principalmente quando fizer push para o github

Veja o .gitignore no passo 2.

---

## 13. Comandos que você realmente vai usar

```bash
git status (verifica o status das modificações)
git add . (adiciona todas as modificações prontas para fazer o commit)
git commit -m "" (cria o seu commit/mensagem da versão do código)
git checkout -b (cria uma nova branch)
git checkout (verifica a branch atual)
git checkout -a (mostra todas as branchs criadas)
git merge (faz o merge de uma branch com a atual)
git log --oneline --graph (mostra o histórico de commits)
git log --oneline (você pode usar sem o --graph também)
git branch (git branch mostra a branch atual de desenvolvimento)
```

---

## 14. Segurança & isolamento

* Sem `remote` configurado
* Sem `git push` que enviaria para o github
* Identidade local
* Histórico só no disco

Verificar:

```bash
git remote -v
# vazio
```

---

## Próximo passo imediato

Crie agora uma branch real:

```bash
git checkout -b feature-teste
```

Trabalhe nela e faça **2 commits pequenos** hoje.
