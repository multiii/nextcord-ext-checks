nextcord-ext-checks
==================

nextcord-ext-checks is a module which implements various decorator
functions, to be used on discord command functions for your discord.py
bot

Installation:
-------------

Installation is done using pip: https://pypi.org/project/nextcord-ext-checks/

.. code:: py

    pip install nextcord-ext-checks

Usage:
------

Starting off, import ``nextcord.ext.checks`` and then you can use its
various decorator functions.

Examples:
~~~~~~~~~

.. code:: py

    from nextcord.ext import checks

    #.. Creating your Discord Bot ...

    """Checking if the author is the Server Owner"""
    @bot.command()
    @checks.is_guild_owner()
    async def foo(ctx):
        await ctx.send(f"{ctx.author.mention} is the Server Owner!")

    """Checking if 3 arguments were passed into the function"""
    @bot.command()
    @checks.has_args(3)
    async def bar(ctx, x, y):
        await ctx.send(f"The result is {x + y}")
        
    """Error Handling"""
    @bar.error
    async def bar_error(ctx, error):
        if isinstance(error, checks.NotEnoughArgs):
            await ctx.send("You have to Enter 3 Arguments (ctx, x, and y) for the command to work")
        else:
            raise error
            
    """Checking if the author's id is in the list of Authorized Members"""
    authorized_members = [394320584089010179, 446670262440820746, 449864700306522112]

    @bot.command()
    @checks.has_user_id_in(authorized_members)
    async def baz(ctx):
        await ctx.send("You are an Authorized Member.")
        
    """Error Handling"""
    @baz.error
    async def baz_error(ctx, error):
        if isinstance(error, checks.MissingID):
            await ctx.send("You are not Authorized.")
        else:
            raise error
            
    bot.run(token)

Notes:
------

-  The Official Documentation: https://multi-yt76.gitbook.io/nextcord-ext-checks/
-  If you need any help related to this module, DM me @Multiii#7676
