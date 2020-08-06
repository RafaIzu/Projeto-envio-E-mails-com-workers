<h1>Aplicativo de envio de e-mail com workers</h1>
<hr>
<br>
<h2>Sobre o projeto:</h2>
<p>Aplicativo no qual simula um envio de e-mail no qual é registrado em um banco de dados postgres. O aplicativo consiste em um frontend no qual possui um formulário no qual possui o um campo para o assunto da mensagem e um outro campo para a mensagem em si. O frontend foi configurado em proxy reverso.</p>
<p> O frontend, no qual é executado em um servidor nginx, encaminha a mensagem e seu titulo para um aplicativo em python 3.6 e depois é persistida em um banco de dados relacional do postgres e ao mesmo tempo que a mensagem é registrada no banco de dados ela também é registrada em uma fila (queue) do redis. Enquanto a fila (queue) tem mensagens para serem enviadas, os workers, escritos em python 3.6, trabalham com várias instancias e assim simulam o o envio de e-mail. Você pode criar vários workers para atender a demanda. </p>
<p>O servidor, o banco de dados, o aplicativo e a fila são dividos em containers separados porém se comunicando entre si</p>
<p>A finalidade do projeto é para o estudo do docker, criação de containers e a comunicação entre containers separados.</p>
<br>
<hr>
<h2>Como instalar:</h2>
<ol>
    <li>Tenha o docker instalado no seu computador</li>
    <li>Após clonar o arquivo, no seu terminal de comando, entre na pasta do projeto e execute o comando "docker-compose up -d --scale worker=3 " para instalar as imagens, criar os containers e criar três workers.</li>
    <li>Execute o comando: "docker-compose logs -f -t worker" para observar a ação dos workers </li>
    <li>Na seu web browser de preferência, digite na barra de endereço apenas "localhost"</li>
    <li>Digite um título para sua mensagem e uma mensagem e clique em enviar</li>
    <li>Observe no seu terminal de comando a ação dos workers. Você pode enviar até três mensagens de uma vez, caso tenha selecionado 3 workers.</li>
    <li>Para ver suas mensagens armazenadas no banco de dados, saia do modo logs com o comando apertando as teclas ctrl + C. Ao retornar no seu terminal de comando, digite o comando: " docker-compose exec db psql -U postgres -d email_sender -c "select * from emails" " para acessar o banco de dados do container.</li>
    <li>Uma tabela deverá aparecer com as informações das mensagens enviadas.</li>
    <li>Para encerrar os containers digite "docker-compose down"</li>
</ol>



