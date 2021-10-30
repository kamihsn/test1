#include <iostream>
#include <cstdio>
#include <string>
#include <queue>
#include <vector>

// Test.cpp : Ce fichier contient la fonction 'main'. L'exécution du programme commence et se termine à cet endroit.
//
using namespace std;

struct noeud {

    char s_donnee;
    double s_freq;
    noeud* s_gauche = NULL;
    noeud* s_droit = NULL;

    noeud(char d, double f, noeud* s_gauche, noeud* s_droit) {

        s_gauche = NULL;
        s_droit = NULL;
        this->s_donnee = d;
        this->s_freq = f;
    }
};

struct compare
{
    bool operator()(noeud* gauche, noeud* droit)
    {
        return gauche->s_freq > droit->s_freq;
    }
};

//stocker les instances des noeuds précédent ds le nouveau noeud crée 
noeud* getNoeud(char s_donnee, double freq, noeud* gauche, noeud* droit)
{
    noeud* node = new noeud(s_donnee, freq, gauche, droit);

    node->s_donnee = s_donnee;
    node->s_freq = freq;
    node->s_gauche = gauche;
    node->s_droit = droit;

    return node;
}

class texte {
    string m_chaine;
    noeud* m_racine = NULL; // arbre huffman
public:
    texte() {};
    texte(string text) {
        m_chaine = text;
    }
    string getMchaine() {
        return m_chaine;
    }

    noeud* getracine() {
        return m_racine;
    }
    void setMchaine(string n) {
        m_chaine = n;
    }

 
    //~texte();

    void Affiche(struct noeud* racine, string chaine) {

        if (racine==NULL) // si le noeud est nul
            return;

        if (racine->s_donnee != '*')
            cout << racine->s_donnee << " : " << chaine << endl;

        Affiche(racine->s_gauche, chaine + '0');
        Affiche(racine->s_droit, chaine + '1');
    }

    void HuffmanCode(char d[], double freq[], int taille) {
        noeud* s_gauche = NULL;
        noeud* s_droit = NULL;
        noeud* tete;
        priority_queue<noeud*, vector<noeud*>, compare> q;

        // Remplissage de la queue
        for (int i = 0; i < taille; i++) {
            q.push(new noeud(d[i], freq[i], s_gauche, s_droit));
        }
        //cout << "" << endl;
        //Extraire les éléments min, les combiner et réinserer
        for (int i = 1; i < taille; i++) {
            s_gauche = q.top();
            q.pop();

            s_droit = q.top();
            q.pop();

            tete = getNoeud('*', s_gauche->s_freq + s_droit->s_freq, s_gauche, s_droit);
            q.push(tete);
        }

        //Affiche(q.top(), "");
        m_racine = q.top(); //Arbre au complet somme freq 28

        //cout << m_racine->s_donnee << endl;*/
    }


};



/*void cleanup(noeud* Noeud) {

    if (Noeud != NULL) {
        cleanup(Noeud->s_gauche);
        cleanup(Noeud->s_droit);

        delete Noeud;
    }
}
*/



int main()
{
    //char data[] = { 'a', 'b', 'c', 'd', 'e', 'f' };
    //char data[] = { 'd','f','b','a','c','e' };
    char data[] = { 'd','f','b'};
    //double freq[] = { 5, 3, 7, 1, 10, 2 };

    //double freq[] = { 1,2,3,5,7,10 }; // ordonné les freq 
    double freq[] = { 1,2,3}; // ordonné les freq 
    texte n(data);
    //cout << n.getMchaine()<< endl;
    n.HuffmanCode(data, freq, sizeof(data));

    //n.Affiche(n.getracine(),"");
    n.Affiche(n.getracine(), "");
    //cout << n.getracine()->s_droit<< endl;


    return 0;
}

// Exécuter le programme : Ctrl+F5 ou menu Déboguer > Exécuter sans débogage
// Déboguer le programme : F5 ou menu Déboguer > Démarrer le débogage

// Astuces pour bien démarrer : 
//   1. Utilisez la fenêtre Explorateur de solutions pour ajouter des fichiers et les gérer.
//   2. Utilisez la fenêtre Team Explorer pour vous connecter au contrôle de code source.
//   3. Utilisez la fenêtre Sortie pour voir la sortie de la génération et d'autres messages.
//   4. Utilisez la fenêtre Liste d'erreurs pour voir les erreurs.
//   5. Accédez à Projet > Ajouter un nouvel élément pour créer des fichiers de code, ou à Projet > Ajouter un élément existant pour ajouter des fichiers de code existants au projet.
//   6. Pour rouvrir ce projet plus tard, accédez à Fichier > Ouvrir > Projet et sélectionnez le fichier .sln.
