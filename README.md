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
 class Startup

    {
        public string FP;
        public string SP;
        public Startup(string Firstname, string secondname)
        {
            FP = Firstname;
            SP = secondname;
        }
        const int Rows = 6, col = 7;
        

        private char[,] area;

        int enteries;

        public Startup()
        {
            area = new char[6, 7];

            for (int i = 0; i < 6; i++)
                for (int j = 0; j < 6; j++)
                    area[i, j] = '*';
        }

        public void gamearea()
        {
            for (int i = 0; i < 6; i++)
            {
                for (int j = 0; j < 7; j++)
                {
                    Console.Write(area[i,j]);
                    Console.Write(' ');
                }
                Console.Write('\n');
            }
        }
        public bool enteriesentered(char player, int column)
        {
            column--;

            if (area[0, column] != '*')
                return false;

            for (int i = 0; i < 6; i++)
            {
                if ((i== 6 - 1) || (area[i + 1, column] != '*'))
                {
                    area[i, column] = player;
                    break;
                }
            }

            enteries++;
            return true;
        }

        public bool connectfouringrid(char player)
        {
                for (int i= 0; i <6; i++)
                for (int j = 0; j < 4; j++)
                    if (area[i, j] == player && area[i, j + 1] == player)
                        if (area[i, j + 2] == player && area[i, j + 3] == player)
                            return true;

            for (int i = 0; i < 3; i++)
                for (int j = 0; j < 7; j++)
                    if (area[i, j] == player && area[i + 1, j] == player)
                        if (area[i + 2, j] == player && area[i + 3, j] == player)
                            return true;

            for (int i = 0; i < 3; i++)
            {
                for (int j= 0; j < 7; j++)
                {

                    if (area[i, j] == player)
                    {


                    }
                }
            }

            return false;
        }

        public bool outoforder()
        {
            return enteries >= 6 * 7;
        }
    }
}
