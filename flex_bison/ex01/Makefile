CC		=	clang
CFLAGS	=	-W -Wall -Wextra
LDFLAGS	=	-ll
LEX		=	flex
RM		=	rm -rf

NAME	=	ex01
TARGET	=	$(NAME).exe

all:	$(TARGET)

$(TARGET):	$(NAME).o
	$(CC) $(LDFLAGS) $< -o $@

clean:
	$(RM) $(NAME).o $(NAME).c

fclean:	clean
	$(RM) $(TARGET)

re:	fclean all

.PHONY:	all clean fclean re