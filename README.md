using System;

namespace Connect4
{
    public class Startup
    {

        public char[,] area;

        int enteries;

        public string FP;
        public string SP;


        public Startup()
        {

            area = new char[6, 7];

            for (int i = 0; i < 6; i++)
                for (int j = 0; j < 6; j++)
                    area[i, j] = '*';
        }





        public Startup(string Firstname, string secondname)
        {
            FP = Firstname;
            SP = secondname;
        }




        public void gamearea()
        {
            for (int i = 0; i < 6; i++)
            {
                for (int j = 0; j < 7; j++)
                {
                    Console.Write(area[i, j]);

                }
                Console.Write('\n');
            }
        }




        public bool enteriesentered(char player, int col)
        {
            col--;

            if (area[0, col] != '*')
                return false;

            for (int i = 0; i < 6; i++)
            {
                if ((i == 6 - 1) || (area[i + 1, col] != '*'))
                {
                    area[i, col] = player;
                    break;
                }
            }

            enteries++;
            return true;
        }





        public bool connectfouringrid(char player)
        {

            for (int y = 0; y < 6; y++)
                for (int x = 0; x < 4; x++)
                    if (area[y, x] == player &&
                        area[y, x + 1] == player &&
                        area[y, x + 2] == player &&
                        area[y, x + 3] == player)

                        return true;

            for (int y = 0; y < 4; y++)
                for (int x = 0; x < 6; x++)
                    if (area[y, x] == player &&
                        area[y + 1, x] == player &&
                        area[y + 2, x] == player &&
                        area[y + 3, x] == player)

                        return true;


            return true;


        }
        
       
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

                char contestant = 'x';
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


                        if (Int32.TryParse(Console.ReadLine(), out Tab))
                        {
                            if (Tab <= 1 && Tab <= 7)
                            {
                                if (play.enteriesentered(contestant, Tab))
                                {
                                    pop = false;
                                }
                                else
                                {
                                    Console.Clear();
                                    play.gamearea();
                                    Console.WriteLine("Enter another number .");
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
                        Console.Write(contestant + "is  winning!");

                        pin = false;
                    }


                    else
                    {
                        contestant = contestant == 'x' ? 'O' : 'x';
                    }
                }

                Console.ReadLine();
            }
        }
    }
}
