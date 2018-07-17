# mardi17juillet
class BoardCase


 attr_accessor :status, :nbre_case

 def initialize(status ="")
  @status = status
  @nbre_case = nbre_case
  @@instances +=1



#first, I defined the new_board method to create and hold variables for empty squares on grid
def new_board
@a1 = " "
@a2 = " "
@a3 = " "
@b1 = " "
@b2 = " "
@b3 = " "
@c1 = " "
@c2 = " "
@c3 = " "
end

#then, I defined the squares method to turn the empty squares into an array
def squares
[@a1, @a2, @a3, @b1, @b2, @b3, @c1, @c2, @c3]

end

def win_combos
[[@a1, @a2, @a3],
[@a1, @b2, @c3],
[@a1, @b1, @c1],
[@b1, @b2, @b3],
[@c1, @c2, @c3],
[@c1, @b2, @a3],
[@a2, @b2, @c2],
[@a3, @b3, @c3]]

end

#the print_grid method draws a picture of the grid that holds the empty spaces from the squares array. 
def print_grid
puts
puts "   1   2   3"
puts "A  #{@a1} | #{@a2} | #{@a3} "
puts "  ---|---|---"
puts "B  #{@b1} | #{@b2} | #{@b3} "
puts "  ---|---|---"
puts "C  #{@c1} | #{@c2} | #{@c3} "
puts
check_for_winner

end

#def method to check if user's choice of move is valid/available. this should be called only after the player has had 3 turns but I don't know how to do that. 
def check_validity square_availability
if square_availability == " "
 true
else
 puts "That space is taken. Get your own!"
end
end

def user_turn
user_choice_hash = {"a1" => @a1,
                   "a2" => @a2,
                   "a3" => @a3,
                   "b1" => @b1,
                   "b2" => @b2,
                   "b3" => @b3,
                   "c1" => @c1,
                   "c2" => @c2,
                   "c3" => @c3}
               

puts "Please choose a square:"
user_choice = gets.chomp.downcase
user_choice_hash.each do |choice, square|
 if user_choice == choice
   if check_validity(square)
     square.sub!(" ", "X")
     print_grid
   end
 elsif user_choice == "q" or user_choice == "quit"
   exit
 end
end
#check_for_winner
end




#check_for_winner

def check_for_winner
win_combos.each do |combos|
 if combos[0] == "O" && combos[1] == "O" && combos[2] == "O"
   puts "#{@secondplayer} a gagné! Bravo!"
   exit
 elsif combos[0] == "X" && combos[1] == "X" && combos[2] == "X"
   puts "#{@firstplayer} a gagné! Bravo!"
   exit
 #else
   #puts "Tie! Enter q to quit game."
 end
end
end

def start_game


   puts "=================================="
   puts "Bienvenue dans mon jeu Tic Tac Toe!"
   puts ""
   puts "comment s'apelle le joueur 1?"
   @firstplayer =gets.chomp
   puts "comment s'apelle le joueur 2?"
   @secondplayer =gets.chomp
   puts "Pour placer votre X sur la grille, entrez l'emplacement (ex - a1, b3)."
   puts "Pour quitter, entrez q à tout moment"
end

def run_game
start_game
new_board
while true
 print_grid
 user_turn

end
end

run_game
