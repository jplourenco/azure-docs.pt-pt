
1. Visite o [Portal do Azure].
2. Clique em **Procurar Tudo** > **Aplicações Móveis** > o back-end que criou.
3. Nas definições da aplicação móvel, clique em **Início Rápido** > **Cordova**.
4. Em **Configurar a aplicação cliente**, selecione **Criar uma Nova Aplicação** e clique em **Transferir**.
2. Descompacte o ficheiro ZIP transferido para um diretório no disco rígido, navegue para o ficheiro de solução (.sln) e abra-o com o Visual Studio.
3. No Visual Studio, escolha a plataforma de solução (Android, iOS ou Windows) a partir da lista pendente junto à seta de início. Selecione um dispositivo de implementação específico ou emulador ao clicar na lista pendente na seta verde. Pode utilizar a plataforma Android e o emulador Ripple predefinidos. Tutoriais mais avançados (por exemplo, notificações push) irão requerer que selecione um dispositivo ou emulador suportados.
4. Para criar e executar a aplicação Cordova, prima F5 ou clique na seta verde. Se for apresentada uma caixa de diálogo de segurança no emulador a solicitar acesso à rede, aceite.
5. Depois de iniciada a aplicação no dispositivo ou no emulador, introduza texto relevante em **Introduzir novo texto**, como *Concluir o tutorial* e, em seguida, clique no botão **Adicionar**.

Os dados de inserções de back-end do pedido encontram-se na tabela TodoItem na Base de Dados SQL e devolvem informações sobre os itens recentemente armazenados na aplicação móvel. A aplicação móvel apresenta estes dados na lista.

![](./media/app-service-mobile-cordova-quickstart/quickstart-startup.png)

Pode repetir os passos 3 a 5 para outras plataformas.

[Portal do Azure]: https://portal.azure.com/


<!--HONumber=Dec16_HO1-->


