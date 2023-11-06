# Construindo-um-Sistema-de-Hospedagem-de-um-Hotel-no-C-
Neste LAB foi proposto um desafio para construir um sistema de hospedagem, que será usado para realizar uma reserva em um hotel


using System;

class Pessoa
{
    public string Nome { get; set; }
    public int Idade { get; set; }
}

class Suíte
{
    public int Número { get; set; }
    public decimal Diária { get; set; }
}

class Reserva
{
    public Pessoa Hóspede { get; set; }
    public Suíte SuíteReservada { get; set; }
    public DateTime DataEntrada { get; set; }
    public DateTime DataSaída { get; set; }

    public int CalcularQuantidadeHóspedes()
    {
        return Hóspede.Idade >= 18 ? 1 : 0;
    }

    public decimal CalcularValorDiária()
    {
        int períodoReserva = (int)(DataSaída - DataEntrada).TotalDays;
        decimal valorTotal = períodoReserva * SuíteReservada.Diária;

        if (períodoReserva > 10)
        {
            // Aplicar desconto de 10% para reservas com mais de 10 dias
            valorTotal *= 0.9m;
        }

        return valorTotal;
    }
}

class Program
{
    static void Main()
    {
        Pessoa hóspede = new Pessoa { Nome = "Alice", Idade = 25 };
        Suíte suíte = new Suíte { Número = 101, Diária = 100.00m };

        Reserva reserva = new Reserva
        {
            Hóspede = hóspede,
            SuíteReservada = suíte,
            DataEntrada = new DateTime(2023, 11, 1),
            DataSaída = new DateTime(2023, 11, 15)
        };

        int quantidadeHóspedes = reserva.CalcularQuantidadeHóspedes();
        decimal valorDiária = reserva.CalcularValorDiária();

        Console.WriteLine($"Quantidade de Hóspedes: {quantidadeHóspedes}");
        Console.WriteLine($"Valor da Diária: {valorDiária:C}");
    }
}
