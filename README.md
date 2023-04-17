# Projeto-Jenkins

Fala galera, este repositório se remete há um caso de estudo, onde quis aprofundar mais meus conhecimentos de **CI/CD**, utilizando uma ótima ferramenta que é o **Jenkins**. O projeto se resume neste seguinte fluxo:

![alt tag](https://github.com/mauropereirafilho/projeto-jenkins/blob/cb1d1053bf5fccf7de9160bb24e4328e26d9fbf7/jenkins.jpg)

* Baseado neste repositório Git, teremos um [Pipeline](https://github.com/mauropereirafilho/projeto-jenkins/blob/main/Jenkinsfile) do **Jenkins**.
* A pipeline valida o repositório, builda a imagem **Docker** baseado no [Dockerfile](https://github.com/mauropereirafilho/projeto-jenkins/blob/main/Docker/Dockerfile) da pasta **Docker**.
* Depois realiza o push da imagem, para nosso [registry](https://hub.docker.com/u/pereirafmauro) do Docker.
* E finaliza, realizando o Deploy desta imagem, em um [Deployment](https://github.com/mauropereirafilho/projeto-jenkins/blob/main/Kubernetes/deployment.yaml) do **Kubernetes**, especificado na pasta **Kubernetes**.

Desta forma, finalizamos de forma unificada, toda a etapa de **CI/CD**, utilizando apenas o **Jenkins**. Sendo o **build**, e o **push** da imagem **Docker**, nossa etapa de **CI**. E o **deploy** no **Kubernetes**, nossa etapa de **CD**.


## Considerações

* O **Jenkins**, serve para realizar todos os procedimentos citados à cima, de maneira totalmente automatizada. Lembrando que o **Jenkins**, **não cria os arquivos**, ele apenas os executa de acordo com o fluxo da pipeline.
* Para instalação do [Jenkins](https://www.jenkins.io/download/)
* Para instalação do [Kubernetes](https://minikube.sigs.k8s.io/docs/start/)
* Após o Jenkins ter sido instalado, precisamos instalar os seguintes plugins, para que nossa pipeline funcione: [KubernetesCLI](https://plugins.jenkins.io/kubernetes-cli/) e [Dockerpipeline](https://plugins.jenkins.io/docker-workflow/).
* O **Jenkins**, realiza todos os procedimentos através do usuário ``jenkins``. Portanto, o mesmo deve possuir as permissões necessárias, para realizar tarefas no Docker. Para fornecer as permissões, utlizaremos o seguinte comando.
```bash
sudo usermod -aG docker jenkins
```
* No arquivo referente a Pipeline, especificamente nas linhas ([22](https://github.com/mauropereirafilho/projeto-jenkins/blob/main/Jenkinsfile#L22), [32](https://github.com/mauropereirafilho/projeto-jenkins/blob/main/Jenkinsfile#L32)), existem variáveis de ambiente, que se remetem ao **Dockerhub** na linha 22, e ao **Kubeconfig** na linha 32. As mesmas devem ser criadas no Jenkins, com os respectivos valores.
 

