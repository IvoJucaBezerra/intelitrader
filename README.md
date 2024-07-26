## Criptografia na rede do navio


A intelitrader foi contratada para traduzir uma mensagem capturada na rede de um navio e ela está criptografada. Não sabemos que tipo de criptografia eles usaram, a única coisa que sabemos até agora, é que, a cada 8 bits, os dois últimos estão invertidos e a cada 4 bits, os 4 bits foram trocados com os próximos 4.


#### Mensagem criptografada:
10010110
11110111
01010110
00000001
00010111
00100110
01010111
00000001
00010111
01110110
01010111
00110110
11110111
11010111
01010111
00000011

#### Instruções:
* De preferência, coloque o código em um arquivo único, para que seja possível executar online e coloque o link do site que executa. Ex: playcode.io/javascript
* Existe mais de uma maneira de resolver este problema, mas aqui está alguns conceitos que podem te ajudar:
  * Tabela ASCII
  * Operadores lógicos
  * Números binários e hexadecimais
* Você saberá se conseguiu descriptografar a mensagem se ela for legível e em inglês. Pois, qualquer bit errado, você terá uma mensagem cheia de símbolos.

# Resolução: 

  * Link para o dotnetfiddle : https://dotnetfiddle.net/

  * Código em Csharp:
````

    using System;
    public class Program
    {
    public static void Main()
    {
        string mensagem = "10010110 11110111 01010110 00000001 00010111 00100110 01010111 00000001 " +
                          "00010111 01110110 01010111 00110110 11110111 11010111 01010111 00000011";

        Console.WriteLine(Descriptografa(mensagem));
        Console.ReadLine();
    }

    static string InverteOsDoisUltimosBits(string byteString)
    {
        string seisPrimeirosBits = byteString.Substring(0, 6);
        string ultimosDoisInvertidos = byteString[6] == '0' ? "1" : "0";
        ultimosDoisInvertidos += byteString[7] == '0' ? "1" : "0";
        return seisPrimeirosBits + ultimosDoisInvertidos;
    }

    static string TrocaACadaQuatroBits(string byteString)
    {
        return byteString.Substring(4, 4) + byteString.Substring(0, 4);
    }

    static string BinarioParaTexto(string[] binario)
    {
        string texto = "";
        foreach (string letra in binario)
        {
            char caractere = (char)Convert.ToInt32(letra, 2);
            texto += caractere;
        }
        return texto;
    }

    static string Descriptografa(string mensagem)
    {
        string[] byteString = mensagem.Split(' ');
        for (int i = 0; i < byteString.Length; i++)
        {
            byteString[i] = InverteOsDoisUltimosBits(byteString[i]);
            byteString[i] = TrocaACadaQuatroBits(byteString[i]);
        }
        return BinarioParaTexto(byteString);
    }
}

````


## Menor distância de dois arrays
* João estava participando de uma competição de programação e lhe foi dado um problema em que ele tinha que encontrar a menor distância entre dois números de dois arrays.

  * Um exemplo seria:

  * Array 1 -> [-1, 5]
  * Array 2 -> [26, 6]
  * A menor distância seria a combinação do número 5 do array 1 com o número 6 do array 2, que seria 1 de distância.

#### Instruções:
* Use arrays com tamanho maiores ou iguais a 10 números.
* De preferência, coloque o código em um arquivo único, para que seja possível executar online e coloque o link do site que executa. Ex: playcode.io/javascript

# Resolução: 

  * Link para o dotnetfiddle : https://dotnetfiddle.net/

  * Código em Csharp:
````
using System;

class Program
{
    static void Main()
    {
        int[] array1 = { -1, 5, 12, 8, 3, 15, 17, 25, 20, 10 };
        int[] array2 = { 100, 200, 300, 400, 500, 600, 700, 800, 900, 999 };

        int menorDistancia = EncontraMenorDistancia(array1, array2);
        Console.WriteLine($"A menor distância é: {menorDistancia}");
    }

    static int EncontraMenorDistancia(int[] array1, int[] array2)
    {
        Array.Sort(array1);
        Array.Sort(array2);

        int i = 0, j = 0;
        int menorDiferenca = int.MaxValue;

        while (i < array1.Length && j < array2.Length)
        {
            int diferenca = Math.Abs(array1[i] - array2[j]);
            if (diferenca < menorDiferenca)
            {
                menorDiferenca = diferenca;
            }


            if (array1[i] < array2[j])
            {
                i++;
            }
            else
            {
                j++;
            }
        }

        return menorDiferenca;
    }
}
````

  
