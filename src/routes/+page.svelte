<script lang="ts">
    import { Input } from '$lib/components/ui/input';
    import { Textarea } from '$lib/components/ui/textarea';
    import { Button } from '$lib/components/ui/button';
    import CheckCheck from 'lucide-svelte/icons/check-check';
    import { Home } from 'lucide-svelte/icons';
    import { fly } from 'svelte/transition';
</script>

<div class="flex flex-col min-h-screen">
    <header class="px-4 lg:px-6 h-14 flex items-center bg-sky-400">
        <a href="#" class="flex items-center justify-center">
            <img src="/logo.png" alt="" width="64" class="mt-8" />
        </a>
        <nav class="ml-auto flex gap-4 sm:gap-6">
            <a href="#" class="text-sm font-medium hover:underline underline-offset-4"> Products </a>
            <a href="#" class="text-sm font-medium hover:underline underline-offset-4"> About </a>
            <a href="#" class="text-sm font-medium hover:underline underline-offset-4"> Contact </a>
        </nav>
    </header>
    <main class="flex-1 flex-wrap">
        <section class="py-12 md:py-24 lg:py-32 xl:py-48">
            <div class="px-4 md:px-6">
                <div class="space-y-2">
                    <h1 class="text-3xl font-bold tracking-tighter sm:text-5xl xl:text-6xl">Pranav Waterproofing Solutions for Your <Home class="inline" /></h1>
                    <p class="text-gray-500 md:text-xl dark:text-gray-400">Protect your home from water damage with our high-quality waterproofing products and services.</p>
                </div>
                <div class="mt-4 flex justify-between space-x-2">
                    <a
                        href="#"
                        class="flex-1 flex items-center justify-center rounded-md bg-green-500 p-3 font-semibold shadow-neutral-400 shadow-md text-gray-50 transition-colors hover:bg-gray-900/90 focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-gray-950 disabled:pointer-events-none disabled:opacity-50 dark:bg-gray-50 dark:text-gray-900 dark:hover:bg-gray-50/90 dark:focus-visible:ring-gray-300"
                    >
                        WhatsApp
                    </a>
                    <a
                        href="tel:9642518564"
                        class="flex-1 flex items-center justify-center rounded-md bg-sky-400 p-3 font-semibold shadow-neutral-400 shadow-md text-gray-50 transition-colors hover:bg-gray-900/90 focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-gray-950 disabled:pointer-events-none disabled:opacity-50 dark:bg-gray-50 dark:text-gray-900 dark:hover:bg-gray-50/90 dark:focus-visible:ring-gray-300"
                    >
                        Call 9642518564
                    </a>
                </div>

                <img src="pranav-banner.jpg" alt="" class="w-full object-cover object-center rounded-lg shadow-md mt-4" />
            </div>
        </section>
        <section class="py-6 px-4 md:py-24 lg:py-32 bg-sky-400">
            <div class="flex flex-col justify-center space-y-4">
                <div class="space-y-2">
                    <h2 class="text-3xl font-bold tracking-tighter sm:text-4xl">Basement Waterproofing</h2>
                    <p class=" md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed dark:text-gray-400">
                        Protect your basement from water damage with our high-performance waterproofing solutions.
                    </p>
                </div>
                <ul class="grid gap-2 py-4">
                    <li class="flex items-center space-x-2 bg-white rounded-md p-2">
                        <CheckCheck class="h-5 w-5 text-green-500" />
                        <span>Prevent leaks and moisture buildup</span>
                    </li>
                    <li class="flex items-center space-x-2 bg-white rounded-md p-2">
                        <CheckCheck class="h-5 w-5 text-green-500" />
                        <span>Improve indoor air quality</span>
                    </li>
                    <li class="flex items-center space-x-2 bg-white rounded-md p-2">
                        <CheckCheck class="h-5 w-5 text-green-500" />
                        <span>Increase the value of your home</span>
                    </li>
                </ul>
                <a
                    href="#"
                    class="inline-flex h-10 items-center justify-center rounded-md bg-gray-900 px-8 text-sm font-medium text-gray-50 shadow transition-colors hover:bg-gray-900/90 focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-gray-950 disabled:pointer-events-none disabled:opacity-50 dark:bg-gray-50 dark:text-gray-900 dark:hover:bg-gray-50/90 dark:focus-visible:ring-gray-300"
                >
                    Learn More
                </a>
                <img
                    src="gallery-basement.webp"
                    width="550"
                    height="310"
                    alt="Basement Waterproofing"
                    class="mx-auto aspect-video overflow-hidden rounded-xl object-cover object-center sm:w-full lg:order-last fade-in shadow-md"
                />
            </div>
            <div class="container px-4 md:px-6"></div>
        </section>
        <section class="py-12 md:py-24 lg:py-32">
            <div class="container px-4 md:px-6">
                <div class="grid gap-6 lg:grid-cols-[500px_1fr] lg:gap-12 xl:grid-cols-[550px_1fr]">
                    <div class="flex flex-col justify-center space-y-4">
                        <div class="space-y-2">
                            <h2 class="text-3xl font-bold tracking-tighter sm:text-4xl">Roof Waterproofing</h2>
                            <p class="text-gray-500 md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed dark:text-gray-400">
                                Protect your roof from water damage and extend its lifespan with our professional waterproofing services.
                            </p>
                        </div>
                        <ul class="grid gap-2 py-4">
                            <li>Prevent leaks and water intrusion</li>
                            <li>Improve energy efficiency</li>
                            <li>Extend the life of your roof</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>
        <section class="py-6 md:py-24 lg:py-32">
            <div class="container px-4 md:px-6">
                <div class="grid gap-6 lg:grid-cols-[1fr_500px] lg:gap-12 xl:grid-cols-[1fr_550px]">
                    <div class="flex flex-col justify-center space-y-4">
                        <div class="space-y-2">
                            <h2 class="text-3xl font-bold tracking-tighter sm:text-4xl">Foundation Waterproofing</h2>
                            <p class="text-gray-500 md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed dark:text-gray-400">
                                Protect your home's foundation from water damage and ensure its structural integrity.
                            </p>
                        </div>
                        <ul class="grid gap-2 py-4">
                            <li>Prevent cracks and foundation settling</li>
                            <li>Improve indoor air quality</li>
                            <li>Increase the value of your home</li>
                        </ul>
                    </div>
                    <img
                        src="/placeholder.svg"
                        width="550"
                        height="310"
                        alt="Foundation Waterproofing"
                        class="mx-auto aspect-video overflow-hidden rounded-xl object-cover object-center sm:w-full lg:order-last"
                    />
                </div>
            </div>
        </section>
        <section class="py-12 md:py-24 lg:py-32 bg-gray-100 dark:bg-gray-800">
            <div class="container px-4 md:px-6">
                <div class="flex flex-col items-center justify-center space-y-4 text-center">
                    <div class="space-y-2">
                        <h2 class="text-3xl font-bold tracking-tighter sm:text-4xl">Get in Touch</h2>
                        <p class="text-gray-500 md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed dark:text-gray-400">
                            Fill out the form below to request a free quote or learn more about our waterproofing solutions.
                        </p>
                    </div>
                    <form class="w-full md:space-y-4">
                        <Input type="text" placeholder="Name" class="w-full" />
                        <Input type="email" placeholder="Email" class="w-full" />
                        <Textarea placeholder="Message" class="w-full" rows={4} />
                        <Button type="submit" class="w-full">Submit</Button>
                    </form>
                </div>
            </div>
        </section>
    </main>
    <footer class="flex flex-col gap-2 sm:flex-row py-6 w-full shrink-0 items-center px-4 md:px-6 border-t">
        <p class="text-xs text-gray-500 dark:text-gray-400">&copy; 2024 Waterproofing Solutions. All rights reserved.</p>
        <nav class="sm:ml-auto flex gap-4 sm:gap-6">
            <a href="#" class="text-xs hover:underline underline-offset-4"> Terms of Service </a>
            <a href="#" class="text-xs hover:underline underline-offset-4"> Privacy Policy </a>
        </nav>
    </footer>
</div>
