class TrieNode
{

	char data;
	boolean isTerminating;
	TrieNode children[];
	int childCount;

        public TrieNode(char data) 
        {
		this.data = data;
		isTerminating = false;
		children = new TrieNode[26];
		childCount = 0;
	}
}


public class Trie 
{

	private TrieNode root;
	public int count;
	public Trie() 
        {
		root = new TrieNode('\0');
		count = 0;
	}	
    
    private boolean SearchWord(TrieNode root, String word) // Assume Trie stores only small characters.
    {
        if(word.length()==0)
        {
            if(root.isTerminating==true)
            {
                return true;
            }
            
            else // if root.isTerminating is false, then that word aint a valid word
            {
                return false;
            }
        }
        
        char ch=word.charAt(0);
        int index=ch-'a';
        
        // Now check whether the root of the TrieNode contains a node with same data
        TrieNode child=root.children[index];
        if(child==null)
        {
            return false;
        }
        
        return SearchWord(child,word.substring(1));
        
    }

    private boolean add(TrieNode root, String word)
    {
	if(word.length() == 0)
        {
		if (root.isTerminating==false) 
                {
			root.isTerminating = true;
			return true;
		} 
            
                else // already true, means root (if word is '', then root is last character) was already made isTerminating true, thus need not be counted again
                {
			return false;
	        }
         }	
	
		int childIndex = word.charAt(0) - 'a';
		TrieNode child = root.children[childIndex];

		if(child == null)
                {
			child = new TrieNode(word.charAt(0));
			root.children[childIndex] = child;
			root.childCount++;
		}
		// If child is not null, then it exists previously, no need to add, don't worry and do anything; just recurse further
                return add(child, word.substring(1));

	}
    }
    
    public static void searchTrie(TrieNode root, String word, String temp)
{    
        // When word/pattern jiske aage autocomplete suggest karwaani hai, ends!
        if(word.length()==0)
        {
            // Print rest of the words.
            TrieNode newNode = new TrieNode('\0'); // create newNode

            int f = 0; // Flag variable in case there are no further nodes.
            ArrayList<Character> ch = new ArrayList<Character>(); // store next characters from current root in the trie
            ArrayList<TrieNode> nodes = new ArrayList<>(); // store all trie nodes next from current
            
            for(int i=0;i<26;i++)
            {
                if(root.children[i]!=null)
                {
                    newNode = root.children[i];
                    boolean ans = root.children[i].isTerminating; 
                    newNode.isTerminating = ans; // this property will be useful for printing
                    
                    nodes.add(newNode);
                    ch.add(newNode.data);
                    f=1;
                }
            }
            
            // If flag variable not used, then iteration will keep on going on giving StackOverflow exception
            if(f==0) 
            {
                return;
            }  
            
            // f==1 meaning there was some node after the current root and our trie has words which use 'word' as base word.
            else
            {
                // ch.size() and nodes.size() will be same
                for(int i=0;i<ch.size();i++) 
                {
                    // Means word+nodes.get(i).data is a valid word and can be shown in autocomplete
                    if(nodes.get(i).isTerminating == true)
                    {
                        System.out.println(temp+ch.get(i));
                    }
                    
                    // Recurse further for all the nodes which were found as children of current root, thus they have a base as word+.... 
                    searchTrie(nodes.get(i),word,temp+ch.get(i)); 
                }
            }
        }
        
        else
        {
        int childIndex = word.charAt(0)-'a';
        TrieNode childNode = root.children[childIndex];
        if(childNode==null)
        {
            return;
        }
        
        searchTrie(childNode,word.substring(1),temp);
            
        }
}
    
public void autoComplete(ArrayList<String> input, String word) 
{
        int flag=0;
        for(int i=0;i<input.size();i++)
        {
            String s = input.get(i);
            
            // If for instance, the word itself is a part of input arraylist, then print it and don't add to arraylist.
            if(s.equals(word) && flag==0)
            {
                System.out.println(word);
                flag=1;
            }

            add(root,s);

        }
        
        // Now that I have added all words in the trie, I can go for autocomplete and use 'temp' for printing output. Minimum output of temp is word+"...."
        String temp = word;
        searchTrie(root,word,temp);
     }
}
	
}
