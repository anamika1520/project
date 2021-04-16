using System;

namespace Connect4
{
    class Program
    {
        static void Main(string[] args)
        {
            Startup play = new Startup();
            Startup names = new Startup();
            Console.WriteLine("Enter the name of first player ");
            string Firstname = Console.ReadLine();

            Console.WriteLine("Enter the name of second player ");
            string SP = Console.ReadLine();


            char contestant = '1';
            int Tab;

            bool pin = true;
            bool pop;

            while (pin)
            {

                Console.Clear();
                play.gamearea();

                do
                {
                    pop = true;

                    Console.WriteLine("\n Turn of Contestant " + contestant + ":");
                    if (Int32.TryParse(Console.ReadLine(), out Tab))
                    {
                        if (1 <= Tab && Tab <= 7)
                        {
                            if (play.enteriesentered(contestant, Tab))
                            {
                                pop = false;
                            }
                            else
                            {
                                Console.Clear();
                                play.gamearea();
                                Console.WriteLine("\nNo much space left in this column .");
                            }
                        }
                        else
                        {
                            Console.Clear();
                            play.gamearea();
                            Console.WriteLine("\nInput integers only between 1 and 7.");
                        }
                    }
                    else
                    {
                        Console.Clear();
                        play.gamearea();
                        Console.WriteLine("\nInput an integer.");
                    }
                } while (pop);

                if (play.connectfouringrid(contestant))
                {
                    Console.Clear();
                    play.gamearea();
                    Console.Write("\nPlayer " + contestant + "HAS WON!!!!!" + "\n Please enter to quit the game ");

                    pin = false;
                }
                else if (play.outoforder())
                {
                    Console.Clear();
                    play.gamearea();
                    Console.WriteLine("\nIt is a draw." + "\nPress enter to quit.");

                    pin = false;
                }
                else
                {
                    contestant = contestant == '1' ? '2' : '1';
                }
            }

            Console.ReadKey();
        }
    }
