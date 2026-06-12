import java.util.Stack;
import java.util.Queue;
import java.util.List;
import java.util.LinkedList;
import java.util.ArrayList;

public class latihan {
    static class Graph {
        int jumlahnode;
        List<List<Integer>>adjancencyList;

        public Graph(int node){
            this.jumlahnode = node;
            adjancencyList = new ArrayList<>(node);
            for(int i = 0; i<node; i++){
                adjancencyList.add(new ArrayList<>());
                
            }
        }

        public void buatEdge(int parent, int child){
            adjancencyList.get(parent).add(child);
        }
    }
    public static void main(String[]args){
        int totalnode = 10;
        Graph graf = new Graph(totalnode);

        graf.buatEdge(0,1);
        graf.buatEdge(0,2);
        graf.buatEdge(1,3);
        graf.buatEdge(1,4);
        graf.buatEdge(2,5);
        graf.buatEdge(2,6);
        graf.buatEdge(3,7);
        graf.buatEdge(4,8);
        graf.buatEdge(5,9);

        int startnode = 0;
        int targetnode = 8;

        System.out.println("================================================");
        System.out.println("Algoritma Pencarian DFS (Depth First Search)");
        System.out.println("================================================");
        algoritmaDFS(graf,startnode,targetnode);

        System.out.println("==================================================");
        System.out.println("Algoritma Pencarian BFS (Breadth First Search)");
        System.out.println("==================================================");
        algoritmaBFS(graf,startnode,targetnode);


    }
    public static void algoritmaDFS(Graph graf, int start, int target){
        boolean[]visited = new boolean[graf.jumlahnode];
        Stack<Integer>stackLifo = new Stack<>();

        stackLifo.push(start);
        System.out.println("\n -> Push Root Node : " + start + " ke Stack LIFO");

        while(!stackLifo.isEmpty()){
            int nodesekarang = stackLifo.pop();
            System.out.println("\n-> Pop Node : " + nodesekarang + " dari atas stack");

            if(!visited[nodesekarang]){
                visited[nodesekarang] = true;
                System.out.println("\n->[DFS]Scanning  a" + nodesekarang);

                if (nodesekarang == target){
                    System.out.println("->Data Ditemukan! a" + target + "menggunakan algoritma DFS");
                    return;
                    
                } 
                List<Integer>child = graf.adjancencyList.get(nodesekarang);
                for(int i = child.size()-1; i>=0; i--){
                    int nodechild = child.get(i);
                    if(!visited[nodechild]){
                        stackLifo.push(nodechild);
                        System.out.println("\n->Push Node Child a" + nodechild + " ke Stack Lifo");
                    }
                    
                }

            }
        }

    }
    public static void algoritmaBFS(Graph graf, int start, int target){
        boolean[] visited = new boolean [graf.jumlahnode];
        Queue<Integer>queueFifo = new LinkedList<>();
        queueFifo.add(start);
        visited[start] = true;

        while(!queueFifo.isEmpty()){
            int nodesekarang = queueFifo.remove();
            System.out.println(" \n--> Remove Node a" + target + " dari antrean");
            System.out.println(" [BFS] Scaning Node a" + nodesekarang );

            if(nodesekarang == target){
                System.out.println (" -> Data Ditemukan! Node a" + target + " menggunakan algoritma BFS");
                return;
            }
            for(int nodechild : graf.adjancencyList.get(nodesekarang)){
                if(! visited[nodechild]){
                    visited[nodechild] = true;
                    queueFifo.add(nodechild);
                    System.out.println("\n-> Add Node Child a" + nodechild + " ke antrean");

                }
            }

        }

       }
}


