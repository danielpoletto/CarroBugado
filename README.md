# CarroBugado
Jogo de carrinho em C#
using System;
using OpenTK;
using OpenTK.Graphics.OpenGL;
using OpenTK.Input;


namespace CarroBugado
{
    class Program : GameWindow
    {
        //    ========== Controles ============
        //Teclas para controlar o CARRO = WSAD;
        //Tecla para Atirar: Barra de espaço (Space);
        //Tecla para Reiniciar o Jogo após "Game Over" = Enter;
        //    ========== Controles ============

        //    ========== Objetivos ============
        // Fugir dos inimigos na COR AMARELO; que causam dano a VIDA;
        // Matar os Inimigos na COR VERDE; se colididos com o CARRO, geram uma especie de dissimulação no "TEMPO/ESPAÇO" aumentando o campo de colisão do CARRO;
        // Matar os Inimigos na COR VERDE; para "corrigir o tamanho do CARRO no "TEMPO/ESPAÇO";
        // Fugir da Colisão com todos os inimigos da TELA;
        // Matar o maximo de inimigos possiveis, futuramente poderá ser adicionado Tempo como modo competitivo;
        //    ========== Objetivos ============

        //==== Meus agradecimentos Ao programador e seu canal do YouTube, pela iniciativa e esforço em ensinar noções de programação! 
        // ========= Like!!! ===========

        //Declaração das Variaves durante a construção do joguinho; muitas delas nem foram tão usadas assim, mas, a criação ocorreu depois de um problema ou de muito pensar em uma sulução; kk :(
        int xDoCarro = 0;
        int yDoCarro = 0;

        int larguraDoCarro = 25;
        int alturaDoCarro = 45;
        int comprimentoDoCanhaoDoCarro = 40;
        int larguraDoCanhaoDoCarro = 8;
        int tamanhoDaRodaDoCarro1Direita = 10;
        int tamanhoDaRodaDoCarro1Esquerda = 10;
        int tamanhoDaRodaDoCarro2Direita = 10;
        int tamanhoDaRodaDoCarro2Esquerda = 10;
        
        int xDoTiro = 0;
        int yDoTiro = 0;
        int xDoTiroFixo = 0;
        int yDoTiroFixo = 0;
        int tamanhoDoTiro = 8;
        int tamanhoDoTiroFixo = 8;
        int tamanhoDoTiroReal = 8;        
        int xDoTiroReal = 0;
        int yDoTiroReal = 0;
        int velocidadeDoTiroEmY = 30;

        int xDoPontilhado = 0;
        int yDoPontilhado = 0;
        int xDoPontilhadoCentro = 0;
        int yDoPontilhadoCentro1 = -190;
        int yDoPontilhadoCentro2 = -120;
        int yDoPontilhadoCentro3 = -50;
        int yDoPontilhadoCentro4 = 20;
        int yDoPontilhadoCentro5 = 90;
        int yDoPontilhadoCentro6 = 160;
        int yDoPontilhadoCentro7 = 230;
        int yDoPontilhadoCentro8 = 300;

        int larguraDoPontilhado = 10;
        int alturaDoPontilhado = 18;
        int velocidadeDoPontilhadoEmY = -5;

        int xDoInimigo = 100;
        int yDoInimigo = 50;
        int xDoInimigo2 = -100;
        int yDoInimigo2 = 50;
        int xDoInimigo3 = -100;
        int yDoInimigo3 = 0;
        int xDoInimigo4 = -225;
        int yDoInimigo4 = 100;
        int xDoInimigo5 = 215;
        int yDoInimigo5 = 150;
        int xDoInimigo6 = 55;
        int yDoInimigo6 = 50;
        int larguraDoInimigo = 20;
        int alturaDoInimigo = 20;
        int velocidadeDoInimigoEmX = 20;
        int velocidadeDoInimigoEmY = -10;
        int velocidadeDoInimigo2EmY = -10;

        int xDaVida = 0;
        int yDaVida = 0;
        int larguraDaVida = 40;
        int alturaDaVida = 4;



        // Aqui criamos o efeito de RUA em movimento, ativando a velocidade dos pontilhados do Centro.
        protected override void OnUpdateFrame(FrameEventArgs e)
        {
            yDoPontilhadoCentro1 = yDoPontilhadoCentro1 + velocidadeDoPontilhadoEmY;
            yDoPontilhadoCentro2 = yDoPontilhadoCentro2 + velocidadeDoPontilhadoEmY;
            yDoPontilhadoCentro3 = yDoPontilhadoCentro3 + velocidadeDoPontilhadoEmY;
            yDoPontilhadoCentro4 = yDoPontilhadoCentro4 + velocidadeDoPontilhadoEmY;
            yDoPontilhadoCentro5 = yDoPontilhadoCentro5 + velocidadeDoPontilhadoEmY;
            yDoPontilhadoCentro6 = yDoPontilhadoCentro6 + velocidadeDoPontilhadoEmY;
            yDoPontilhadoCentro7 = yDoPontilhadoCentro7 + velocidadeDoPontilhadoEmY;
            yDoPontilhadoCentro8 = yDoPontilhadoCentro8 + velocidadeDoPontilhadoEmY;


            //Adicionando movimento para os inimigos (de 1 a 2) que se movimentam no eixo X e Y;
            yDoInimigo = yDoInimigo + velocidadeDoInimigoEmY;
            yDoInimigo2 = yDoInimigo2 + velocidadeDoInimigo2EmY;

            //Adicionando movimento para os inimigos (de 3 a 6) que se movimentam no eixo Y somente;
            yDoInimigo3 = yDoInimigo3 + velocidadeDoInimigo2EmY;
            yDoInimigo4 = yDoInimigo4 + velocidadeDoInimigo2EmY;
            yDoInimigo5 = yDoInimigo5 + velocidadeDoInimigo2EmY;
            yDoInimigo6 = yDoInimigo6 + velocidadeDoInimigo2EmY;


            //Aqui faz a verificação de "quanto andou cada pontilado do Centro" e após andar 70, ele retorna a posição inicial, gerando efeito de rua em movimento;
            if (yDoPontilhadoCentro1 - alturaDoPontilhado / 2 < -190 - 70)
            {
                yDoPontilhadoCentro1 = -190;
            }
            if (yDoPontilhadoCentro2 - alturaDoPontilhado / 2 < -120 - 70)
            {
                yDoPontilhadoCentro2 = -120;
            }
            if (yDoPontilhadoCentro3 - alturaDoPontilhado / 2 < -50 - 70)
            {
                yDoPontilhadoCentro3 = -50;
            }
            if (yDoPontilhadoCentro4 - alturaDoPontilhado / 2 < 20 - 70)
            {
                yDoPontilhadoCentro4 = 20;
            }
            if (yDoPontilhadoCentro5 - alturaDoPontilhado / 2 < 90 - 70)
            {
                yDoPontilhadoCentro5 = 90;
            }
            if (yDoPontilhadoCentro6 - alturaDoPontilhado / 2 < 160 - 70)
            {
                yDoPontilhadoCentro6 = 160;
            }
            if (yDoPontilhadoCentro7 - alturaDoPontilhado / 2 < 230 - 70)
            {
                yDoPontilhadoCentro7 = 230;
            }
            if (yDoPontilhadoCentro8 - alturaDoPontilhado / 2 < 230 - 70)
            {
                yDoPontilhadoCentro8 = 230;
            }

            // Adicionando as teclas para digirir o carro bem como sua velocidade quando esta tecla for acionada;
            if (Keyboard.GetState().IsKeyDown(Key.D))
            {
                xDoCarro = xDoCarro + 8;                
            }
            if (Keyboard.GetState().IsKeyDown(Key.A))
            {
                xDoCarro = xDoCarro - 8;
            }
            if (Keyboard.GetState().IsKeyDown(Key.W))
            {
                yDoCarro = yDoCarro + 5;
            }
            if (Keyboard.GetState().IsKeyDown(Key.S))
            {
                yDoCarro = yDoCarro - 5;
            }
            //cria uma ilusão de gif para o tiro, como se ele estivesse saindo da basuca kk =(
            if (Keyboard.GetState().IsKeyDown(Key.Space))
            {
                yDoTiro = yDoTiro + velocidadeDoTiroEmY;
                if (yDoTiro > -ClientSize.Height / 2 + 270)// Ñ sei se este IF fica certo aqui dentro, mas vai q vai.. x.x
                {
                    yDoTiro = 0;
                }
            }
            //Fazendo o Tiro real na cor preto correr no eixo Y, meio "invisivel" para simular metralhadora, visto que o Player pode estar segurando a tecla Space direto.. kk
            if (Keyboard.GetState().IsKeyDown(Key.Space))
            {
                yDoTiroReal = yDoTiroReal + velocidadeDoTiroEmY;
                if (yDoTiroReal > -ClientSize.Height / 2 + 400)
                {
                    yDoTiroReal = 0;                    
                }
                // aqui acionar a colisao do tiro real com os inimigos(do 3 ao 6) que descem no eixo Y e reiniciar sua posição inicial (consegui apenas dentro do IF que verifica se o Space esta apertado)
                if (yDoCarro + yDoTiroReal + 80 > yDoInimigo3 - alturaDoInimigo / 2 - -ClientSize.Height / 2 + ClientSize.Height
                    && xDoInimigo3 + larguraDoInimigo / 2 > xDoCarro + xDoTiroReal - tamanhoDoTiroReal / 2
                    && xDoInimigo3 - larguraDoInimigo / 2 < xDoCarro + xDoTiroReal + tamanhoDoTiroReal / 2)
                {
                    //Volta o inimigo a posição inicial dele
                    yDoInimigo3 = 0;
                    //Após matar o inimigo, devolver os status inicial dele
                    comprimentoDoCanhaoDoCarro = 40;
                    tamanhoDoTiroReal = 8;
                    tamanhoDoTiro = 8;
                    larguraDoCarro = 25;
                }
                if(yDoCarro + yDoTiroReal - 10 > yDoInimigo3 - alturaDoInimigo / 2 - -ClientSize.Height / 2 + ClientSize.Height
                    && xDoInimigo4 + larguraDoInimigo / 2 > xDoCarro + xDoTiroReal - tamanhoDoTiroReal / 2
                    && xDoInimigo4 - larguraDoInimigo / 2 < xDoCarro + xDoTiroReal + tamanhoDoTiroReal / 2)
                {
                    yDoInimigo4 = 100;
                    //Após matar o inimigo, devolver os status inicial dele
                    comprimentoDoCanhaoDoCarro = 40;
                    tamanhoDoTiroReal = 8;
                    tamanhoDoTiro = 8;
                    larguraDoCarro = 25;
                }
                if (yDoCarro + yDoTiroReal - 60 > yDoInimigo3 - alturaDoInimigo / 2 - -ClientSize.Height / 2 + ClientSize.Height
                    && xDoInimigo5 + larguraDoInimigo / 2 > xDoCarro + xDoTiroReal - tamanhoDoTiroReal / 2
                    && xDoInimigo5 - larguraDoInimigo / 2 < xDoCarro + xDoTiroReal + tamanhoDoTiroReal / 2)
                {
                    yDoInimigo5 = 150;
                    //Após matar o inimigo, devolver os status inicial dele
                    comprimentoDoCanhaoDoCarro = 40;
                    tamanhoDoTiroReal = 8;
                    tamanhoDoTiro = 8;
                    larguraDoCarro = 25;
                }
                if (yDoCarro + yDoTiroReal + 40 > yDoInimigo3 - alturaDoInimigo / 2 - -ClientSize.Height / 2 + ClientSize.Height
                    && xDoInimigo6 + larguraDoInimigo / 2 > xDoCarro + xDoTiroReal - tamanhoDoTiroReal / 2
                    && xDoInimigo6 - larguraDoInimigo / 2 < xDoCarro + xDoTiroReal + tamanhoDoTiroReal / 2)
                {
                    yDoInimigo6 = 50;
                    //Após matar o inimigo, devolver os status inicial dele
                    comprimentoDoCanhaoDoCarro = 40;
                    tamanhoDoTiroReal = 8;
                    tamanhoDoTiro = 8;
                    larguraDoCarro = 25;
                }

            }

            //Aqui é criado os colisores em torno da Tela, que não permite o CARRO acessar as areas além do que se Vê; empurrando o CARRO para a PISTA novamente; 
            if (xDoCarro - larguraDoCarro / 2 < -ClientSize.Width / 2)
            {
                xDoCarro = -ClientSize.Width / 2 + 50;
            }
            if (xDoCarro + larguraDoCarro / 2 > ClientSize.Width / 2)
            {
                xDoCarro = ClientSize.Width / 2 - 50;
            }
            if (yDoCarro + alturaDoCarro / 2 > ClientSize.Height)
            {
                yDoCarro = ClientSize.Height - 30;
            }
            if (yDoCarro - alturaDoCarro / 2 < -ClientSize.Height / 2 + 170)
            {
                yDoCarro = -ClientSize.Height / 2 + 200;
            }

            // Inverte a Velocidade do inimigo no eixo X e Y 

            if (yDoInimigo - alturaDoInimigo / 2 < ClientSize.Height)
            {
                xDoInimigo = xDoInimigo + velocidadeDoInimigoEmX;
            }
            if (yDoInimigo2 - alturaDoInimigo / 2 < ClientSize.Height)
            {
                xDoInimigo2 = xDoInimigo2 + velocidadeDoInimigoEmX;
            }
            // Assim que o inimigo aparace na Tela, é acionado os colisores laterais
            if (xDoInimigo + larguraDoInimigo / 2 > ClientSize.Width)
            {
                velocidadeDoInimigoEmX = -velocidadeDoInimigoEmX;
            }
            if (xDoInimigo - larguraDoInimigo / 2 < -ClientSize.Width)
            {
                velocidadeDoInimigoEmX = -velocidadeDoInimigoEmX;
            }
            if (xDoInimigo2 + larguraDoInimigo / 2 > ClientSize.Width)
            {
                velocidadeDoInimigoEmX = -velocidadeDoInimigoEmX;
            }
            if (xDoInimigo2 - larguraDoInimigo / 2 < -ClientSize.Width)
            {
                velocidadeDoInimigoEmX = -velocidadeDoInimigoEmX;
            }
            //Aqui acionamos os colisores do eixo Y, para os inimigos 1 e 2 voltar depois que descer; esses viajam no eixo E e Y;
            if (yDoInimigo - alturaDoInimigo / 2 < -ClientSize.Height * 2)
            {
                velocidadeDoInimigoEmY = -velocidadeDoInimigoEmY;
                yDoInimigo = yDoInimigo + ClientSize.Height * 2 - 20;
                velocidadeDoInimigoEmY = -velocidadeDoInimigoEmY;
            }
            if (yDoInimigo2 - alturaDoInimigo / 2 < -ClientSize.Height * 2)
            {
                velocidadeDoInimigoEmY = -velocidadeDoInimigoEmY;
                yDoInimigo2 = yDoInimigo2 + ClientSize.Height * 2 - 20;
                velocidadeDoInimigoEmY = -velocidadeDoInimigoEmY;
            }

            //Aqui adicionamos a regra para os inimigos3+ que poderá somente viajar no eixo Y
            if (yDoInimigo3 - alturaDoInimigo / 2 < -ClientSize.Height * 2)
            {
                velocidadeDoInimigo2EmY = -velocidadeDoInimigo2EmY;
                yDoInimigo3 = yDoInimigo3 + ClientSize.Height * 2;
                velocidadeDoInimigo2EmY = -velocidadeDoInimigo2EmY;
            }
            if (yDoInimigo4 - alturaDoInimigo / 2 < -ClientSize.Height * 2)
            {
                velocidadeDoInimigo2EmY = -velocidadeDoInimigo2EmY;
                yDoInimigo4 = yDoInimigo4 + ClientSize.Height * 2;
                velocidadeDoInimigo2EmY = -velocidadeDoInimigo2EmY;
            }
            if (yDoInimigo5 - alturaDoInimigo / 2 < -ClientSize.Height * 2)
            {
                velocidadeDoInimigo2EmY = -velocidadeDoInimigo2EmY;
                yDoInimigo5 = yDoInimigo5 + ClientSize.Height * 2;
                velocidadeDoInimigo2EmY = -velocidadeDoInimigo2EmY;
            }
            if (yDoInimigo6 - alturaDoInimigo / 2 < -ClientSize.Height * 2)
            {
                velocidadeDoInimigo2EmY = -velocidadeDoInimigo2EmY;
                yDoInimigo6 = yDoInimigo6 + ClientSize.Height * 2;
                velocidadeDoInimigo2EmY = -velocidadeDoInimigo2EmY;
            }

            //Aqui os efeitos de colisão entre os inimigos de 3 a 6 no Player, empurrando o carro para trás e para o lado quando colidir;
            if (yDoInimigo3 - alturaDoInimigo / 2 < yDoCarro + alturaDoCarro / 2 - ClientSize.Height / 2 - 450
                && yDoInimigo3 + alturaDoInimigo / 2 > yDoCarro + alturaDoCarro / 2 - ClientSize.Height / 2 - 450
                && xDoInimigo3 + larguraDoInimigo / 2 > xDoCarro - larguraDoCarro / 2
                && xDoInimigo3 - larguraDoInimigo / 2 < xDoCarro + larguraDoCarro / 2)            
            {
                comprimentoDoCanhaoDoCarro = 25;
                tamanhoDoTiroReal = 4;
                tamanhoDoTiro = 4;
                larguraDoCarro = 100;
                xDoCarro = xDoCarro + 10;
                yDoCarro = yDoCarro - 40;
            }
            if (yDoInimigo4 - alturaDoInimigo / 2 < yDoCarro + alturaDoCarro / 2 - ClientSize.Height / 2 - 450
                && yDoInimigo4 + alturaDoInimigo / 2 > yDoCarro + alturaDoCarro / 2 - ClientSize.Height / 2 - 450
                && xDoInimigo4 + larguraDoInimigo / 2 > xDoCarro - larguraDoCarro / 2
                && xDoInimigo4 - larguraDoInimigo / 2 < xDoCarro + larguraDoCarro / 2)
            {
                comprimentoDoCanhaoDoCarro = 25;
                tamanhoDoTiroReal = 4;
                tamanhoDoTiro = 4;
                larguraDoCarro = 100;
                xDoCarro = xDoCarro + 10;
                yDoCarro = yDoCarro - 40;
            }
            if (yDoInimigo5 - alturaDoInimigo / 2 < yDoCarro + alturaDoCarro / 2 - ClientSize.Height / 2 - 450
                && yDoInimigo5 + alturaDoInimigo / 2 > yDoCarro + alturaDoCarro / 2 - ClientSize.Height / 2 - 450
                && xDoInimigo5 + larguraDoInimigo / 2 > xDoCarro - larguraDoCarro / 2
                && xDoInimigo5 - larguraDoInimigo / 2 < xDoCarro + larguraDoCarro / 2)
            {
                comprimentoDoCanhaoDoCarro = 25;
                tamanhoDoTiroReal = 4;
                tamanhoDoTiro = 4;
                larguraDoCarro = 100;
                xDoCarro = xDoCarro + 10;
                yDoCarro = yDoCarro - 40;
            }
            if (yDoInimigo6 - alturaDoInimigo / 2 < yDoCarro + alturaDoCarro / 2 - ClientSize.Height / 2 - 450
                && yDoInimigo6 + alturaDoInimigo / 2 > yDoCarro + alturaDoCarro / 2 - ClientSize.Height / 2 - 450
                && xDoInimigo6 + larguraDoInimigo / 2 > xDoCarro - larguraDoCarro / 2
                && xDoInimigo6 - larguraDoInimigo / 2 < xDoCarro + larguraDoCarro / 2)
            {
                comprimentoDoCanhaoDoCarro = 25;
                tamanhoDoTiroReal = 4;
                tamanhoDoTiro = 4;
                larguraDoCarro = 100;
                xDoCarro = xDoCarro + 10;
                yDoCarro = yDoCarro - 40;
            }

            
            //Aqui os efeitos de colisão entre os inimigos de 1 a 2 no Player, empurrando o carro para trás;            
            if (xDoInimigo - larguraDoInimigo / 2 < xDoCarro + larguraDoCarro / 2
                && xDoInimigo + larguraDoInimigo / 2 > xDoCarro - larguraDoCarro / 2
                && yDoInimigo - alturaDoInimigo / 2 + ClientSize.Height < yDoCarro + alturaDoCarro / 2 - 200
                && yDoInimigo + alturaDoInimigo / 2 + ClientSize.Height > yDoCarro - alturaDoCarro / 2 - 200)
            {
                    larguraDaVida = larguraDaVida - 4;
                    yDoCarro = yDoCarro - 40;               
            }
            if (xDoInimigo2 - larguraDoInimigo / 2 < xDoCarro + larguraDoCarro / 2
                && xDoInimigo2 + larguraDoInimigo / 2 > xDoCarro - larguraDoCarro / 2
                && yDoInimigo2 - alturaDoInimigo / 2 + ClientSize.Height < yDoCarro + alturaDoCarro / 2 - 200
                && yDoInimigo2 + alturaDoInimigo / 2 + ClientSize.Height > yDoCarro - alturaDoCarro / 2 - 200)
            {
                larguraDaVida = larguraDaVida - 4;
                yDoCarro = yDoCarro - 40;
            }


            //Aqui fazemos uma analise do Tamanho da Vida, se a Vida Zerar, o Jogo "para", entra em um laço infinito de não executar mais nada kk
            //Seria o GAME OVER do jogo;
            for (int i = 0; i <= 0; i++)
            {
                i = larguraDaVida;//Aqui ocorre o "GAME OVER"; i recebe valor da Vida e checa, se valor for igual ou abaixo de Zero, o jogo PARA, "GAME OVER";
                if (Keyboard.GetState().IsKeyDown(Key.Enter))//Aqui ocorre a verificação dentro do For se a tecla Enter está pressionada, se SIM, a vida Recebe mais 40 "pontos", saindo do laço do For, retornando o jogo inicial; 
                {

                    if (larguraDaVida <= 0)
                    {
                        larguraDaVida = 40;

                    }
                }
            }

            

        }
                                           
               

        protected override void OnRenderFrame(FrameEventArgs e)
        {
            GL.Viewport(0, 0, ClientSize.Width, ClientSize.Height);

            Matrix4 projection = Matrix4.CreateOrthographic(ClientSize.Width, ClientSize.Height, 0.0f, 1.0f);
            GL.MatrixMode(MatrixMode.Projection);
            GL.LoadMatrix(ref projection);

            GL.Clear(ClearBufferMask.ColorBufferBit);

            //Desenhando os pontilhados no CENTRO da TELA;
            DesenharPontilhado(xDoPontilhadoCentro, yDoPontilhadoCentro8, larguraDoPontilhado, alturaDoPontilhado, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhadoCentro, yDoPontilhadoCentro7, larguraDoPontilhado, alturaDoPontilhado, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhadoCentro, yDoPontilhadoCentro6, larguraDoPontilhado, alturaDoPontilhado, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhadoCentro, yDoPontilhadoCentro5, larguraDoPontilhado, alturaDoPontilhado, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhadoCentro, yDoPontilhadoCentro4, larguraDoPontilhado, alturaDoPontilhado, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhadoCentro, yDoPontilhadoCentro3, larguraDoPontilhado, alturaDoPontilhado, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhadoCentro, yDoPontilhadoCentro2, larguraDoPontilhado, alturaDoPontilhado, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhadoCentro, yDoPontilhadoCentro1, larguraDoPontilhado, alturaDoPontilhado, 1.0f, 1.0f, 1.0f);

            //Desenhando os pontilhados como Moldura da RUA;
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + 230, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + 200, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + 170, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + 140, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + 110, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + 80, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + 50, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + 20, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + -230, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + -200, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + -170, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + -140, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + -110, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + -80, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + -50, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado - 270, yDoPontilhado + -20, 1, 10, 1.0f, 1.0f, 1.0f);

            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + 230, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + 200, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + 170, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + 140, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + 110, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + 80, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + 50, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + 20, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + -230, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + -200, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + -170, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + -140, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + -110, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + -80, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + -50, 1, 10, 1.0f, 1.0f, 1.0f);
            DesenharPontilhado(xDoPontilhado + 270, yDoPontilhado + -20, 1, 10, 1.0f, 1.0f, 1.0f);


            //Desenhando o CARRO e seus componentes;
            DesenharCarro(xDoCarro, yDoCarro - 200, larguraDoCarro, alturaDoCarro, 0.0f, 0.0f, 1.0f);
            DesenharRoda1Esquerda(xDoCarro - larguraDoCarro / 2 - 6, yDoCarro - 200 + alturaDoCarro / 2 - tamanhoDaRodaDoCarro1Esquerda - 1 / 2, tamanhoDaRodaDoCarro1Esquerda, tamanhoDaRodaDoCarro1Esquerda, 1.0f, 1.0f, 0.0f);
            DesenharRoda1Direita(xDoCarro + larguraDoCarro / 2 + 6, yDoCarro - 200 + alturaDoCarro / 2 - tamanhoDaRodaDoCarro1Direita - 1 / 2, tamanhoDaRodaDoCarro1Direita, tamanhoDaRodaDoCarro1Direita, 1.0f, 1.0f, 0.0f);
            DesenharRoda2Esquerda(xDoCarro - larguraDoCarro / 2 - 6, yDoCarro - 200 - alturaDoCarro / 2 + tamanhoDaRodaDoCarro2Esquerda + 1 / 2, tamanhoDaRodaDoCarro2Esquerda, tamanhoDaRodaDoCarro2Esquerda, 1.0f, 1.0f, 0.0f);
            DesenharRoda2Direita(xDoCarro + larguraDoCarro / 2 + 6, yDoCarro - 200 - alturaDoCarro / 2 + tamanhoDaRodaDoCarro2Direita + 1 / 2, tamanhoDaRodaDoCarro2Direita, tamanhoDaRodaDoCarro2Direita, 1.0f, 1.0f, 0.0f);
            DesenharCanhao(xDoCarro, yDoCarro - 200 + alturaDoCarro / 2 - 8, larguraDoCanhaoDoCarro, comprimentoDoCanhaoDoCarro, 0.9f, .5f, 1.0f);

            //Desenhando a VIDA;
            DesenharVida(xDaVida + xDoCarro, yDaVida + yDoCarro - 235, larguraDaVida, alturaDaVida, 1.0f, 0.0f, 0.0f);

            
            //Desenhando os quadrados que ficam parados no centro do CARRO; e os Quadrados "TIRO" que sobem para gerar efeito de metralhadora;
            DesenharTiroFixo(xDoTiroFixo + xDoCarro, yDoTiroFixo + yDoCarro - 200 + alturaDoCarro / 2 - 8, tamanhoDoTiroFixo, tamanhoDoTiroFixo, 0.9f, 0.9f, 0.9f);
            DesenharTiroFixo(xDoTiroFixo + xDoCarro, yDoTiroFixo + yDoCarro - 205 + alturaDoCarro / 2 - 8, tamanhoDoTiroFixo, tamanhoDoTiroFixo, 0.1f, 0.1f, 0.1f);
            DesenharTiroFixo(xDoTiroFixo + xDoCarro, yDoTiroFixo + yDoCarro - 225 + alturaDoCarro / 2 - 8, tamanhoDoTiroFixo, tamanhoDoTiroFixo, 0.1f, 0.1f, 0.1f);
            DesenharTiroFixo(xDoTiroFixo + xDoCarro, yDoTiroFixo + yDoCarro - 230 + alturaDoCarro / 2 - 8, tamanhoDoTiroFixo, tamanhoDoTiroFixo, 0.9f, 0.9f, 0.9f);
            DesenharTiro(xDoTiro + xDoCarro, yDoTiro + yDoCarro - 170 + alturaDoCarro / 2 - 14, tamanhoDoTiro, tamanhoDoTiro, 0.3f, 0.4f, 0.1f);
            DesenharTiro(xDoTiro + xDoCarro, yDoTiro + yDoCarro - 170 + alturaDoCarro / 2 - 16, tamanhoDoTiro, tamanhoDoTiro, 0.0f, 0.0f, 0.0f);

            DesenharTiro(xDoTiroReal + xDoCarro, yDoTiroReal + yDoCarro - 200 + alturaDoCarro / 2 - 8, tamanhoDoTiroReal, tamanhoDoTiroReal, 0.1f, 0.0f, 0.1f);


            //Desenhando todos os inimigos;
            DesenharInimigo(xDoInimigo, yDoInimigo + ClientSize.Height, larguraDoInimigo, alturaDoInimigo, 1.0f, 1.0f, 0.0f);
            DesenharInimigo(xDoInimigo2, yDoInimigo2, larguraDoInimigo, alturaDoInimigo, 1.0f, 1.0f, 0.0f);
            DesenharInimigo(xDoInimigo3, yDoInimigo3 + ClientSize.Height, larguraDoInimigo, alturaDoInimigo, 0.0f, 1.0f, 0.0f);
            DesenharInimigo(xDoInimigo4, yDoInimigo4 + ClientSize.Height, larguraDoInimigo, alturaDoInimigo, 0.0f, 1.0f, 0.0f);
            DesenharInimigo(xDoInimigo5, yDoInimigo5 + ClientSize.Height, larguraDoInimigo, alturaDoInimigo, 0.0f, 1.0f, 0.0f);
            DesenharInimigo(xDoInimigo6, yDoInimigo6 + ClientSize.Height, larguraDoInimigo, alturaDoInimigo, 0.0f, 1.0f, 0.0f);

            //Me perdoe os BUGs que possam existir e a fadiga de códigos, não está Orientado a Objeto;

            // Enjoy~~!! :)

            //Meus agradecimentos Ao programador e seu canal do YouTube, pela iniciativa e esforço em ensinar noções de programação! 
            //Like!!!

            SwapBuffers();
        }


        void DesenharCarro(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(0.5 * larguraDoCarro + x, 0.5 * alturaDoCarro + y);
            GL.Vertex2(0.5 * larguraDoCarro + x, -0.5 * alturaDoCarro + y);
            GL.Vertex2(-0.5 * larguraDoCarro + x, -0.5 * alturaDoCarro + y);
            GL.Vertex2(-0.5 * larguraDoCarro + x, 0.5 * alturaDoCarro + y);
            GL.End();

        }
        void DesenharRoda1Esquerda(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(0.5 * tamanhoDaRodaDoCarro1Esquerda + x, 0.5 * tamanhoDaRodaDoCarro1Esquerda + y);
            GL.Vertex2(0.5 * tamanhoDaRodaDoCarro1Esquerda + x, -0.5 * tamanhoDaRodaDoCarro1Esquerda + y);
            GL.Vertex2(-0.5 * tamanhoDaRodaDoCarro1Esquerda + x, -0.5 * tamanhoDaRodaDoCarro1Esquerda + y);
            GL.Vertex2(-0.5 * tamanhoDaRodaDoCarro1Esquerda + x, 0.5 * tamanhoDaRodaDoCarro1Esquerda + y);
            GL.End();
        }
        void DesenharRoda1Direita(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(0.5 * tamanhoDaRodaDoCarro1Direita + x, 0.5 * tamanhoDaRodaDoCarro1Direita + y);
            GL.Vertex2(0.5 * tamanhoDaRodaDoCarro1Direita + x, -0.5 * tamanhoDaRodaDoCarro1Direita + y);
            GL.Vertex2(-0.5 * tamanhoDaRodaDoCarro1Direita + x, -0.5 * tamanhoDaRodaDoCarro1Direita + y);
            GL.Vertex2(-0.5 * tamanhoDaRodaDoCarro1Direita + x, 0.5 * tamanhoDaRodaDoCarro1Direita + y);
            GL.End();
        }
        void DesenharRoda2Esquerda(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(0.5 * tamanhoDaRodaDoCarro2Esquerda + x, 0.5 * tamanhoDaRodaDoCarro2Esquerda + y);
            GL.Vertex2(0.5 * tamanhoDaRodaDoCarro2Esquerda + x, -0.5 * tamanhoDaRodaDoCarro2Esquerda + y);
            GL.Vertex2(-0.5 * tamanhoDaRodaDoCarro2Esquerda + x, -0.5 * tamanhoDaRodaDoCarro2Esquerda + y);
            GL.Vertex2(-0.5 * tamanhoDaRodaDoCarro2Esquerda + x, 0.5 * tamanhoDaRodaDoCarro2Esquerda + y);
            GL.End();
        }
        void DesenharRoda2Direita(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(0.5 * tamanhoDaRodaDoCarro2Direita + x, 0.5 * tamanhoDaRodaDoCarro2Direita + y);
            GL.Vertex2(0.5 * tamanhoDaRodaDoCarro2Direita + x, -0.5 * tamanhoDaRodaDoCarro2Direita + y);
            GL.Vertex2(-0.5 * tamanhoDaRodaDoCarro2Direita + x, -0.5 * tamanhoDaRodaDoCarro2Direita + y);
            GL.Vertex2(-0.5 * tamanhoDaRodaDoCarro2Direita + x, 0.5 * tamanhoDaRodaDoCarro2Direita + y);
            GL.End();
        }

        void DesenharVida(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(0.5 * larguraDaVida + x, 0.5 * alturaDaVida + y);
            GL.Vertex2(0.5 * larguraDaVida + x, -0.5 * alturaDaVida + y);
            GL.Vertex2(-0.5 * larguraDaVida + x, -0.5 * alturaDaVida + y);
            GL.Vertex2(-0.5 * larguraDaVida + x, 0.5 * alturaDaVida + y);
            GL.End();
        }

        void DesenharCanhao(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(0.5 * larguraDoCanhaoDoCarro + x, 0.5 * comprimentoDoCanhaoDoCarro + y);
            GL.Vertex2(0.5 * larguraDoCanhaoDoCarro + x, -0.5 * comprimentoDoCanhaoDoCarro + y);
            GL.Vertex2(-0.5 * larguraDoCanhaoDoCarro + x, -0.5 * comprimentoDoCanhaoDoCarro + y);
            GL.Vertex2(-0.5 * larguraDoCanhaoDoCarro + x, 0.5 * comprimentoDoCanhaoDoCarro + y);
            GL.End();

        }

        void DesenharInimigo(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(-0.9f * largura + x, -0.3f * altura + y);
            GL.Vertex2(-0.3f * largura + x, 0.3f * altura + y);
            GL.Vertex2(0.3f * largura + x, 0.3f * altura + y);
            GL.Vertex2(0.9f * largura + x, -0.3f * altura + y);
            GL.End();
        }

        void DesenharPontilhado(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(-0.5f * largura + x, -0.5f * altura + y);
            GL.Vertex2(-0.5f * largura + x, 0.5f * altura + y);
            GL.Vertex2(0.5f * largura + x, 0.5f * altura + y);
            GL.Vertex2(0.5f * largura + x, -0.5f * altura + y);
            GL.End();

        }

        void DesenharTiro(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(-0.5f * largura + x, -0.5f * altura + y);
            GL.Vertex2(-0.5f * largura + x, 0.5f * altura + y);
            GL.Vertex2(0.5f * largura + x, 0.5f * altura + y);
            GL.Vertex2(0.5f * largura + x, -0.5f * altura + y);
            GL.End();
        }

        void DesenharTiroFixo(int x, int y, int largura, int altura, float r, float g, float b)
        {
            GL.Color3(r, g, b);

            GL.Begin(PrimitiveType.Quads);
            GL.Vertex2(-0.5f * largura + x, -0.5f * altura + y);
            GL.Vertex2(-0.5f * largura + x, 0.5f * altura + y);
            GL.Vertex2(0.5f * largura + x, 0.5f * altura + y);
            GL.Vertex2(0.5f * largura + x, -0.5f * altura + y);
            GL.End();
        }

        static void Main()
        {

            new Program().Run();


        }
    }
}

