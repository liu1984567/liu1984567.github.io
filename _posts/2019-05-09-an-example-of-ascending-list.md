---
layout: post
title:  "an example of an ascending list!"
date:   2019-05-09 21:50:29
categories: jekyll update
---
the code below:

{% highlight ruby %}
#include <stdio.h>
#include <stdlib.h>

struct s_inc_node{
	unsigned ui_val;
	struct s_inc_node *next;
};

struct s_inc_node *add_node(struct s_inc_node *p_list, struct s_inc_node *node)
{
	struct s_inc_node *p_newlist = p_list;
	struct s_inc_node *pre = NULL;
	struct s_inc_node *curr = p_list;
	while (NULL != curr && node->ui_val >= curr->ui_val)
	{
		pre = curr;
		curr = curr->next;
	}

	if (NULL == pre)
	{
		p_newlist = node;
		node->next = curr;
	}
	else
	{
		pre->next = node;
		node->next = curr;
	}

	return p_newlist;
}

struct s_inc_node *remove_node(struct s_inc_node *p_list, struct s_inc_node *node)
{
	struct s_inc_node *pre = NULL;
	struct s_inc_node *curr = p_list;
	while (NULL != curr)
	{
		if (curr == node)
		{
			if (NULL == pre)
				p_list = curr->next;
			else
				pre->next = curr->next;
			break;
		}

		pre = curr;
		curr = curr->next;
	}

	return p_list;
}

void dump_inc_list(struct s_inc_node *p_list)
{
	printf("dump this list\r\n");
	printf("+++++++++++++++++++++++++++++++\r\n");
	struct s_inc_node* curr = p_list;
	while(NULL != curr)
	{
		printf("%u ", curr->ui_val);
		curr = curr->next;
	}

	printf("\r\n");
}

void test_single_node(struct s_inc_node *p_list, unsigned ui_count)
{
	struct s_inc_node* p_node0 = p_list + (ui_count / 2);
	struct s_inc_node* p_node1 = p_node0 + 1;
	struct s_inc_node* p_node2 = p_node0 - 1;

	struct s_inc_node* p_tmplist = add_node(p_node0, p_node1);
	dump_inc_list(p_tmplist);
	p_tmplist = add_node(p_node0, p_node2);
	dump_inc_list(p_tmplist);
	p_tmplist = add_node(p_node0, p_node0);
	dump_inc_list(p_tmplist);
}
void test_delete_node(struct s_inc_node *p_list, unsigned ui_count)
{
	struct s_inc_node* p_node0 = p_list + (ui_count / 2);
	struct s_inc_node* p_node1 = p_node0 + 1;
	struct s_inc_node* p_node2 = p_node0 - 1;

	struct s_inc_node* p_tmplist = remove_node(p_node2, p_node0);
	dump_inc_list(p_tmplist);
	p_tmplist = add_node(p_node2, p_node0);
	dump_inc_list(p_tmplist);
	p_tmplist = remove_node(p_node2, p_node1);
	dump_inc_list(p_tmplist);
	p_tmplist = remove_node(p_node2, p_node2);
	dump_inc_list(p_tmplist);
	p_tmplist = remove_node(p_node0, p_node0);
	dump_inc_list(p_tmplist);
}

#define NODE_COUNT (10)
void main()
{
	struct s_inc_node  nodearr[NODE_COUNT];
	struct s_inc_node* p_list = NULL;
	struct s_inc_node* p_node = NULL;
	int i;
	for (i = 0; i < NODE_COUNT; i++)
	{
		nodearr[i].ui_val = i;
		nodearr[i].next = NULL;
	}

	test_single_node(nodearr, NODE_COUNT);
	test_delete_node(nodearr, NODE_COUNT);
}

{% endhighlight %}


