Este é um aplicativo desenvolvido em Python utilizando a biblioteca Tkinter para criar uma interface gráfica amigável, que permite aos usuários gerar arquivos PDF personalizados. Com esse aplicativo, os usuários podem definir várias configurações, como o caminho de uma fonte TrueType (TTF), tamanho da fonte, margens da página e o texto que desejam incluir no PDF.

O aplicativo possui os seguintes componentes:

Caminho da Fonte (TTF): Os usuários podem especificar o caminho para uma fonte TrueType (TTF) que desejam usar no PDF.

Tamanho da Letra: Define o tamanho da fonte a ser usada no PDF.

Margens Esquerda, Superior, Direita e Inferior (em centímetros): Permite aos usuários configurar as margens da página.

Texto do PDF: Os usuários podem inserir o texto que desejam incluir no PDF. O aplicativo substitui automaticamente as quebras de linha por <br/>.

Nome do Arquivo: Os usuários podem fornecer um nome para o arquivo PDF de saída. Se o nome não incluir a extensão ".pdf", o aplicativo a adicionará automaticamente. Além disso, se o nome do arquivo já existir na pasta de saída escolhida, o aplicativo adicionará um número à frente do nome do arquivo para evitar a sobregravação.

Botão "Gerar PDF": Ao clicar neste botão, o aplicativo gera o arquivo PDF com base nas configurações definidas pelos usuários.

Resultado: O aplicativo fornece um feedback ao usuário, indicando se o PDF foi gerado com sucesso ou se ocorreu um erro.

O aplicativo utiliza a biblioteca ReportLab para criar o arquivo PDF com base nas configurações fornecidas. Ele permite que os usuários personalizem as configurações da página e o conteúdo do PDF de acordo com suas necessidades.

Em resumo, este aplicativo fornece uma maneira fácil de criar PDFs personalizados, tornando-o útil para tarefas que envolvem a criação de documentos PDF com formatação personalizada, como relatórios, documentos, ou qualquer conteúdo que requer formatação específica em um arquivo PDF.
