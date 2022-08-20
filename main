#include <cstring>
#include <vector>
#include <bits/stdc++.h>
#include <cstring>
#include <algorithm>
#include <string>
using namespace std;

unsigned width = 3;             //width of board
unsigned height = 3;            //height of board
vector<string> vecOfStr;
vector<string>::iterator it;
struct Results
{
    const char* const* Words;    // pointers to unique found words, each terminated by a non-alpha char
    unsigned           Count;    // number of words found
    unsigned           Score;    // total score
    void*              UserData; // ignored by test framework; can use for your own purposes
};

int points;                                               //track score
typedef std::vector<std::string> VectorOfStrings_type;   //vector of strings to store words from file   
VectorOfStrings_type words { };                          //global vector of type words
class ResultsWrapper                                    //To store words of type pointer to words
{
private:
                                // construct and maintain memory so the pointers in the Result struct will be valid
    char ** Words;
    unsigned int Count;

public:
    ResultsWrapper(const VectorOfStrings_type &input){
        Count = input.size();

                                // create the array of pointers
        Words = static_cast<char**>(
            malloc(Count * sizeof(char*)) 
        );

        // create each string
        for (unsigned int i = 0; i < Count; ++i){
            const std::string &name = input[i];

            // allocate space
            Words[i] = static_cast<char*>(
                malloc(name.size() + 1)
            );

            // copy string
            strncpy(Words[i], name.data(), name.size());

            // add null terminator
            Words[i][name.size()] = '\0';
        }
    }

    operator Results (){
        return Results{ Words, Count };
    }

    ~ResultsWrapper(){

    }
};


void LoadDictionary(const char* filepath)               //Load dictionary
{

        ifstream ifs = ifstream(filepath, ios_base::in);
        string str;
        if (ifs.is_open() == true) 
        {
                while (getline(ifs, str))
                {
    
                        if(str.size() > 0)
                        {
                                vecOfStr.push_back(str);
                        }        
                }
                ifs.close(); 
      
        }
        else
        {
                cout<< "File could not be open!" <<endl;
                //return 0;
        }  
}
void FreeDictionary()                              //Free memory
{
        vecOfStr.clear();
        
}
bool isWord(string& str)                          //check if words generated match the words of dictionary               
{
    for(it=vecOfStr.begin(); it<vecOfStr.end(); it++)
    {   
        if (str.compare(*it) == 0)               //compare string with words from file
        {
            return true;
        }
    }
    return false; 
     
}
 
// A recursive function to print all words present on board
int findWordsrec(vector<string> boggle1, vector< vector<bool> > visited, int i,
                   int j, string& str,int M, int N)
{

    static int score=0;             //keep track of score
    string u="u";
    visited[i][j] = true;
    str = str + boggle1[i][j];
    if( ('q' == boggle1[i][j]) && (boggle1[i][j+1] != 'u') )             //Boggle 'qu' cube logic
    {
        str=str+u;
    }
    int c;
    if (isWord(str))                                  //check if word is in dictionary file
    {
        words.push_back(str);
        c=str.size();
        //cout<<str<<endl;
        if(c == 3 or c==4)
        {
            score=score+1;
            //cout<<count;
        }
        else if(c == 5)
        {
            score=score+2;
        }
        else if(c == 6)
        {
            score=score+3;
        }
        else if(c == 7)
        {
            score=score+5;
        }
        else if(c >= 8)
        {
            score=score+11;
        }
    }    


    for (int row = i - 1; row <= i + 1 && row < M; row++)
        for (int col = j - 1; col <= j + 1 && col < N; col++)
            if (row >= 0 && col >= 0 && !visited[row][col])
                findWordsUtil(boggle1, visited, row, col, str,M,N);
 

    str.erase(str.length() - 1);
    visited[i][j] = false;
    return score;
}
 

Results findWords(const char* board,unsigned width, unsigned height)
{
    int M= width;
    int N= height;
    int count=0;
    vector<string> boggle1(width);
    int score1;
    vector< vector< bool > > visited( width, vector<bool>( height, false ) );
    string str = "";
    for(int i=0;i<boggle1.size();i++)           // add characters from string to board
    {
        for(int j=0;j<boggle1.size();j++)
        {
            boggle1[i].push_back(board[count]);
            count=count+1;
        }                      
    }
    for(int i=0;i<boggle1.size();i++)           //display the board
    {
        cout<<"\n";
        for(int j=0;j<boggle1.size();j++)
        {
            cout<<boggle1[i][j]<<" ";
            //cout<<endl;
       
        }                      
    }
    cout<<"\n";
    for (int i = 0; i < width; i++)
        for (int j = 0; j < height; j++)
                score1=findWordsUtil(boggle1, visited, i, j, str,M,N);   //function to generate word combinations
                
    points=score1;
    ResultsWrapper temp{ words };                       //Wrapper for storing struct element Words
    return temp;                                        //return struct Results object
}


void FreeWords(Results results1)
{

    cout<<"Number of Words:"<<results1.Count<<endl;
    cout<<"Words:"<<endl;
    for (unsigned int i = 0; i < results1.Count; ++i)
    {
        std::cout << results1.Words[i] << std::endl;
    }    
    results1.Score=points;
    cout<<"Score:"<<results1.Score<<endl;    
}



int main()
{
    const char* filepath = "file.txt";
    struct Results r1;
    string board;
    LoadDictionary(filepath);
    r1=findWords(board1,width,height);        //Function that returns Structure object with all results
    FreeWords(r1);                            //Function to Display results
    FreeDictionary();                       // Free memory
    return 0;
}
