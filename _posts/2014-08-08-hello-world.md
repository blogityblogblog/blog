---
layout: post
title: "Hello World"
modified:
categories: blog
excerpt:
tags: []
image:
  feature:
date: 2017-03-19T15:39:55-04:00
modified: 2017-03-19T14:19:19-04:00
---

Hi You'll find this post in your `_posts` directory - edit this post and re-build (or run with the `-w` switch) to see your changes!
To add new posts, simply add a file in the `_posts` directory that follows the convention: YYYY-MM-DD-name-of-post.ext.

{% highlight csharp %}
static void Main(string[] args)
        {
            var connString = ConfigurationManager.ConnectionStrings["playground"].ToString();
            try
            {
                using (var conn = new SqlConnection(connString))
                using (var cmd = new SqlCommand())
                {
                    conn.Open();
                    cmd.Connection = conn;
                    cmd.CommandText = "usp_getItemPrices";
                    cmd.CommandType = System.Data.CommandType.StoredProcedure;

                    var results = new List<String>();
                    var rdr = cmd.ExecuteReader();

                    while (rdr.Read())
                    {
                        results.Add(string.Format("{0} costs ${1} with a {2}% discount applied.", rdr["Item"], rdr["DiscountedPrice"], rdr["DiscountApplied"]));
                    }

                    if (results.Any())
                    {
                        foreach (var result in results)
                        {
                            Console.WriteLine(result);
                        }
                    }
                    else
                    {
                        Console.WriteLine("No Results");
                    }
                }
            }
            catch (SqlException ex)
            {
                Console.WriteLine(ex.Message);
            }
            Console.Read();
        }
{% endhighlight %}

## Sample Heading

### Sample Heading 2

Jekyll also offers powerful support for code snippets:

```ruby
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
```

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll]:    http://jekyllrb.com
