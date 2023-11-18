# Exercicio1-ED-2023-2.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int saque ( unsigned int *restrict notas,
            const unsigned int *restrict valores,
            unsigned int nvalores,
            unsigned int valor )
{
  // Zera os contadores.
  memset ( notas, 0, nvalores * sizeof ( int ) );

  for ( int i = 0; i < nvalores; i++ )
  {
    // casos especiais
    // Problemas com R$ 6,00 e R$ 8,00 restantes...
    if ( valores[i] == 5 )
    {
      // Assume que o último elemento equivale às
      // notas de R$ 2,00
      if ( valor == 6 )
      {
        notas[nvalores - 1] = 3;
        valor = 0;
        break;
      }
      else if ( valor == 8 )
      {
        notas[nvalores - 1] = 4;
        valor = 0;
        break;
      }
    }

    while ( valor >= valores[i] )
    {
      notas[i]++;
      valor -= valores[i];
    }
  }

  return valor == 0;
}

int main ( void )
{
  static const unsigned int valores[7] = { 200, 100, 50, 20, 10, 5, 2 };
  unsigned int notas[7];
  unsigned int valor;

  fputs ( "Quantidade desejada: ", stdout );
  fflush ( stdout );

  if ( scanf ( "%u", &valor ) == 1 )
  {
    if ( ! saque ( notas, valores, 7, valor ) )
    {
    error:
      fputs ( "Valor inválido.\n", stdout );
      return EXIT_FAILURE;
    }

    // Mostrar notas.
    for ( int i = 0; i < 7; i++ )
      printf ( "R$ %3u,00 -> %u notas.\n", valores[i], notas[i] );
  }
  else
    goto error;

  return EXIT_SUCCESS;
}


