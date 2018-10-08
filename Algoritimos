#include <stdio.h>
#include <iostream>
#include <vector>
#include <string>
#include <time.h>
#include <sys\timeb.h>
#include <windows.h>
#include <locale.h>

using namespace std;

int *vetor1, *vetor2, *vetor3, *vetor4, *vetor5,
*vetor6, *vetor7, *vetor8, *vetor9, *vetor10,
*vetor11, *vetor12, *vetor13, *vetor14, *vetor15;

double tDecorrido = 0.000;


int* ler_vetor(char* url){

	FILE *arq;

	arq = fopen(url, "r");
	if(arq == NULL)
			printf("Erro, nao foi possivel abrir o arquivo\n");

    int numero, linhas = 0, i = 0, maior, menor;

		while((fscanf(arq,"%d\n", &numero))!=EOF)
             linhas++;

        int* vet = new int[linhas];
        rewind(arq);


		while((fscanf(arq,"%d\n", &numero))!=EOF){
            vet[i] = numero;
            //cout << vet[i] << endl;
            i++;

		}

		fclose(arq);

		return vet;

}

int retornaTam(char* url){
    FILE *arq;

	arq = fopen(url, "r");
	if(arq == NULL)
			printf("Erro, nao foi possivel abrir o arquivo\n");

    int numero, linhas = 0;

		while((fscanf(arq,"%d\n", &numero))!=EOF)
             linhas++;

    fclose(arq);

    return linhas;
}

double PCFreq = 0.0;
__int64 CounterStart = 0;

void StartCounter(){
    LARGE_INTEGER li;
    if(!QueryPerformanceFrequency(&li))
        printf("QueryPerformanceFrequency Failed.\n");
    PCFreq = (double)(li.QuadPart) / 1000.0;
    QueryPerformanceCounter(&li);
    CounterStart = li.QuadPart;
}

double GetCounter(){
    LARGE_INTEGER li;
    QueryPerformanceCounter(&li);
    return (double)(li.QuadPart - CounterStart) / PCFreq;
}

void insertionSort(int* original, int length) {
	int i, j, atual;
	for (i = 1; i < length; i++) {
		atual = original[i];
		for (j = i - 1; (j >= 0) && (atual < original[j]); j--) {
			original[j + 1] = original[j];
        }
		original[j+1] = atual;
	}
}

void SelectionSort(int* vetor, int tam) {
    for (int indice = 0; indice < tam; ++indice) {
        int indiceMenor = indice;
        for (int indiceSeguinte = indice+1; indiceSeguinte < tam; ++indiceSeguinte) {
            if (vetor[indiceSeguinte] < vetor[indiceMenor]) {
                indiceMenor = indiceSeguinte;
            }
        }
        int aux = vetor[indice];
        vetor[indice] = vetor[indiceMenor];
        vetor[indiceMenor] = aux;
    }
}

void bubbleSort(int* vet, int length) {
	int i, j, temp;

	for (i = 0; i < length - 1; i++){
        for (j = (i+1); j < length; j++){
            if (vet[j] < vet[i]){
                temp = vet[i];
                vet[i] = vet[j];
                vet[j] = temp;
            }
        }
    }
}

void shellSort(int *vet, int size) {
    int i , j , value;
    int gap = 1;
    while(gap < size) {
        gap = 3*gap+1;
    }
    while ( gap > 1) {
        gap /= 3;
        for(i = gap; i < size; i++) {
            value = vet[i];
            j = i;
            while (j >= gap && value < vet[j - gap]) {
                vet[j] = vet [j - gap];
                j = j - gap;
            }
            vet [j] = value;
        }
    }
}

void merge(int vetor[], int comeco, int meio, int fim) {
    int com1 = comeco, com2 = meio+1, comAux = 0, tam = fim-comeco+1;
    int *vetAux;
    vetAux = (int*)malloc(tam * sizeof(int));

    while(com1 <= meio && com2 <= fim){
        if(vetor[com1] < vetor[com2]) {
            vetAux[comAux] = vetor[com1];
            com1++;
        } else {
            vetAux[comAux] = vetor[com2];
            com2++;
        }
        comAux++;
    }

    while(com1 <= meio){  //Caso ainda haja elementos na primeira metade
        vetAux[comAux] = vetor[com1];
        comAux++;
        com1++;
    }

    while(com2 <= fim) {   //Caso ainda haja elementos na segunda metade
        vetAux[comAux] = vetor[com2];
        comAux++;
        com2++;
    }

    for(comAux = comeco; comAux <= fim; comAux++){    //Move os elementos de volta para o vetor original
        vetor[comAux] = vetAux[comAux-comeco];
    }

    free(vetAux);
}

void mergeSort(int vetor[], int comeco, int fim){
    if (comeco < fim) {
        int meio = (fim+comeco)/2;

        mergeSort(vetor, comeco, meio);
        mergeSort(vetor, meio+1, fim);
        merge(vetor, comeco, meio, fim);
    }
}

void quick_sort(int *a, int left, int right) {
    int i, j, x, y;

    i = left;
    j = right;
    x = a[(left + right) / 2];

    while(i <= j) {
        while(a[i] < x && i < right) {
            i++;
        }
        while(a[j] > x && j > left) {
            j--;
        }
        if(i <= j) {
            y = a[i];
            a[i] = a[j];
            a[j] = y;
            i++;
            j--;
        }
    }

    if(j > left) {
        quick_sort(a, left, j);
    }
    if(i < right) {
        quick_sort(a, i, right);
    }
}

void heapsort(int* a, int n) {
   int i = n / 2, pai, filho, t;
   while(true) {
      if (i > 0) {
          i--;
          t = a[i];
      } else {
          n--;
          if (n == 0) return;
          t = a[n];
          a[n] = a[0];
      }
      pai = i;
      filho = i * 2 + 1;
      while (filho < n) {
          if ((filho + 1 < n)  &&  (a[filho + 1] > a[filho]))
              filho++;
          if (a[filho] > t) {
             a[pai] = a[filho];
             pai = filho;
             filho = pai * 2 + 1;
          } else {
             break;
          }
      }
      a[pai] = t;
   }
}



void chamadaInsertion(){

        StartCounter();
		insertionSort(vetor1, retornaTam("entrada10.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Insertion Sort - Dez: %.4lf segundos\n", tDecorrido);

		StartCounter();
		insertionSort(vetor2, retornaTam("entrada1000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Insertion Sort - Mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		insertionSort(vetor3, retornaTam("entrada10000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Insertion Sort - Dez mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		insertionSort(vetor4, retornaTam("entrada1e+05.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Insertion Sort - Cem mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		insertionSort(vetor5, retornaTam("entrada1e+06.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Insertion Sort - Um milhão: = %.4lf segundos\n", (double)tDecorrido/1000);

        }
void chamadaSelection(){

StartCounter();
		SelectionSort(vetor1, retornaTam("entrada10.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Selection Sort - Dez: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		SelectionSort(vetor2, retornaTam("entrada1000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Selection Sort - Mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		SelectionSort(vetor3, retornaTam("entrada10000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Selection Sort - Dez mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		SelectionSort(vetor4, retornaTam("entrada1e+05.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Selection Sort - Cem mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		SelectionSort(vetor5, retornaTam("entrada1e+06.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Selection Sort - Um milhão: = %.4lf segundos\n", (double)tDecorrido/1000);


}
void chamadaShell(){

        StartCounter();
		shellSort(vetor1, retornaTam("entrada10.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Shell Sort - Dez: %.4lf segundos\n", tDecorrido);

		StartCounter();
		shellSort(vetor2, retornaTam("entrada1000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Shell Sort - Mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		shellSort(vetor3, retornaTam("entrada10000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Shell Sort - Dez mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		shellSort(vetor4, retornaTam("entrada1e+05.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Shell Sort - Cem mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		shellSort(vetor5, retornaTam("entrada1e+06.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Shell Sort - Um milhão: = %.4lf segundos\n", (double)tDecorrido/1000);

}
void chamadaBubble(){

        StartCounter();
		bubbleSort(vetor1, retornaTam("entrada10.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Bubble Sort - Dez: %.4lf segundos\n", tDecorrido);

		StartCounter();
		bubbleSort(vetor2, retornaTam("entrada1000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Bubble Sort - Mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		bubbleSort(vetor3, retornaTam("entrada10000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Bubble Sort - Dez mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		bubbleSort(vetor4, retornaTam("entrada1e+05.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Bubble Sort - Cem mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		bubbleSort(vetor5, retornaTam("entrada1e+06.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Bubble Sort - Um milhão: = %.4lf segundos\n", (double)tDecorrido/1000);

}
void chamadaQuick(){



StartCounter();
		quick_sort(vetor1, 0, retornaTam("entrada10.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Quick Sort - Dez: %.4lf segundos\n", tDecorrido);

		StartCounter();
		quick_sort(vetor2, 0, retornaTam("entrada1000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Quick Sort - Mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		quick_sort(vetor3, 0, retornaTam("entrada10000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Quick Sort - Dez mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		quick_sort(vetor4, 0, retornaTam("entrada1e+05.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Quick Sort - Cem mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		quick_sort(vetor5, 0, retornaTam("entrada1e+05.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Quick Sort - Um milhao: = %.4lf segundos\n", (double)tDecorrido/1000);


}
void chamadaMerge(){

        StartCounter();
		mergeSort(vetor1, 0, 10);
		tDecorrido = GetCounter();
		printf("Tempo Merge Sort - Dez: %.4lf segundos\n", tDecorrido);

		StartCounter();
		mergeSort(vetor2, 0, 1000);
		tDecorrido = GetCounter();
		printf("Tempo Merge Sort - Mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		mergeSort(vetor3, 0, 10000);
		tDecorrido = GetCounter();
		printf("Tempo Merge Sort - Dez mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		mergeSort(vetor4, 0, 100000);
		tDecorrido = GetCounter();
		printf("Tempo Merge Sort - Cem mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		mergeSort(vetor5, 0, 1000000);
		tDecorrido = GetCounter();
		printf("Tempo Merge Sort - Um milhão: = %.4lf segundos\n", (double)tDecorrido/1000);
}
void chamadaHeap(){

        StartCounter();
		heapsort(vetor1, retornaTam("entrada10.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Heapsort - Dez: %.4lf segundos\n", tDecorrido);

		StartCounter();
		heapsort(vetor2, retornaTam("entrada1000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Heapsort - Mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		heapsort(vetor3, retornaTam("entrada10000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Heapsort - Dez mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		heapsort(vetor4, retornaTam("entrada1e+05.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Heapsort - Cem mil: = %.4lf segundos\n", (double)tDecorrido/1000);

		StartCounter();
		heapsort(vetor5, retornaTam("entrada1e+06.txt"));
		tDecorrido = GetCounter();
		printf("Tempo Heapsort - Um milhão: = %.4lf segundos\n", (double)tDecorrido/1000);


}


int main(){

    setlocale(LC_ALL, "Portuguese");
    system("Color D");

		int i;

        clock_t tInicio, tFim;

        //Vetores Aleatorios
        vetor1 = ler_vetor("entrada10.txt");
		vetor2 = ler_vetor("entrada1000.txt");
		vetor3 = ler_vetor("entrada10000.txt");
		vetor4 = ler_vetor("entrada1e+05.txt");
		vetor5 = ler_vetor("entrada1e+06.txt");

        //Vetores Crescentes
		vetor6 = ler_vetor("CrescenteEntrada10.txt");
		vetor7 = ler_vetor("CrescenteEntrada1000.txt");
		vetor8 = ler_vetor("CrescenteEntrada10000.txt");
		vetor9 = ler_vetor("CrescenteEntrada100000.txt");
		vetor10 = ler_vetor("CrescenteEntrada1000000.txt");

        //Vetores Descrescentes
		vetor6 = ler_vetor("CrescenteEntrada10.txt");
		vetor7 = ler_vetor("CrescenteEntrada1000.txt");
		vetor8 = ler_vetor("CrescenteEntrada10000.txt");
		vetor9 = ler_vetor("CrescenteEntrada100000.txt");
		vetor10 = ler_vetor("CrescenteEntrada1000000.txt");

		vetor11 = ler_vetor("DecrescenteEntrada10.txt");
		vetor12 = ler_vetor("DecrescenteEntrada1000.txt");
		vetor13 = ler_vetor("DecrescenteEntrada10000.txt");
		vetor14 = ler_vetor("DecrescenteEntrada100000.txt");
		vetor15 = ler_vetor("DecrescenteEntrada1000000.txt");



        /*for(int i = 0; i<50; i++)
            cout << vetor15[i] << endl;*/

            //Podemos testar dessa forma (onde os vetores contidos na funcao sao aleatorios)
            chamadaShell();

            //Ou pode chamar assim tambem e passar o vetor dessejado respeitando o
            //arquivo correspondente ou o tamanho. (no caso, vetor2 tem espaço pra 1000)

        StartCounter();
		shellSort(vetor2, retornaTam("entrada1000.txt"));
		tDecorrido = GetCounter();
		printf("Tempo ShellSort - Mil: = %.4lf segundos\n", (double)tDecorrido/1000);



return 0;

}


